---
title: 'Tutorial: Azure Active Directory integration with Montage Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Montage Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5c5e8c6f-e4fb-43fe-8841-e371f568ebed
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2018
ms.author: jeedes
ms.openlocfilehash: e11c97ecb33c1b1a37891a521c0375b39ad8a956
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856272"
---
# <a name="tutorial-azure-active-directory-integration-with-montage-online"></a><span data-ttu-id="91f69-103">Tutorial: Azure Active Directory integration with Montage Online</span><span class="sxs-lookup"><span data-stu-id="91f69-103">Tutorial: Azure Active Directory integration with Montage Online</span></span>

<span data-ttu-id="91f69-104">In this tutorial, you learn how to integrate Montage Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91f69-104">In this tutorial, you learn how to integrate Montage Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91f69-105">Integrating Montage Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="91f69-105">Integrating Montage Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91f69-106">You can control in Azure AD who has access to Montage Online.</span><span class="sxs-lookup"><span data-stu-id="91f69-106">You can control in Azure AD who has access to Montage Online.</span></span>
- <span data-ttu-id="91f69-107">You can enable your users to automatically get signed-on to Montage Online (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="91f69-107">You can enable your users to automatically get signed-on to Montage Online (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="91f69-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91f69-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="91f69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="91f69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91f69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91f69-110">Prerequisites</span></span>

<span data-ttu-id="91f69-111">To configure Azure AD integration with Montage Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="91f69-111">To configure Azure AD integration with Montage Online, you need the following items:</span></span>

- <span data-ttu-id="91f69-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="91f69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91f69-113">A Montage Online single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="91f69-113">A Montage Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91f69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="91f69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91f69-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="91f69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91f69-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="91f69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91f69-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91f69-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91f69-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="91f69-118">Scenario description</span></span>
<span data-ttu-id="91f69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="91f69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91f69-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="91f69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91f69-121">Adding Montage Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="91f69-121">Adding Montage Online from the gallery</span></span>
1. <span data-ttu-id="91f69-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91f69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-montage-online-from-the-gallery"></a><span data-ttu-id="91f69-123">Adding Montage Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="91f69-123">Adding Montage Online from the gallery</span></span>
<span data-ttu-id="91f69-124">To configure the integration of Montage Online into Azure AD, you need to add Montage Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="91f69-124">To configure the integration of Montage Online into Azure AD, you need to add Montage Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91f69-125">**To add Montage Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91f69-125">**To add Montage Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91f69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91f69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="91f69-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="91f69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91f69-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91f69-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="91f69-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="91f69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="91f69-133">In the search box, type **Montage Online**, select **Montage Online** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="91f69-133">In the search box, type **Montage Online**, select **Montage Online** from result panel then click **Add** button to add the application.</span></span>

    ![Montage Online in the results list](./media/montageonline-tutorial/tutorial_montageonline_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="91f69-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91f69-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="91f69-136">In this section, you configure and test Azure AD single sign-on with Montage Online based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91f69-136">In this section, you configure and test Azure AD single sign-on with Montage Online based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91f69-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Montage Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91f69-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Montage Online is to a user in Azure AD.</span></span> <span data-ttu-id="91f69-138">In other words, a link relationship between an Azure AD user and the related user in Montage Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="91f69-138">In other words, a link relationship between an Azure AD user and the related user in Montage Online needs to be established.</span></span>

<span data-ttu-id="91f69-139">To configure and test Azure AD single sign-on with Montage Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="91f69-139">To configure and test Azure AD single sign-on with Montage Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91f69-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="91f69-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="91f69-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91f69-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="91f69-142">**[Create a Montage Online test user](#create-a-montage-online-test-user)** - to have a counterpart of Britta Simon in Montage Online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="91f69-142">**[Create a Montage Online test user](#create-a-montage-online-test-user)** - to have a counterpart of Britta Simon in Montage Online that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="91f69-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91f69-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="91f69-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="91f69-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="91f69-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91f69-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="91f69-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Montage Online application.</span><span class="sxs-lookup"><span data-stu-id="91f69-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Montage Online application.</span></span>

<span data-ttu-id="91f69-147">**To configure Azure AD single sign-on with Montage Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91f69-147">**To configure Azure AD single sign-on with Montage Online, perform the following steps:**</span></span>

1. <span data-ttu-id="91f69-148">In the Azure portal, on the **Montage Online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="91f69-148">In the Azure portal, on the **Montage Online** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="91f69-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91f69-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/montageonline-tutorial/tutorial_montageonline_samlbase.png)

1. <span data-ttu-id="91f69-152">On the **Montage Online Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91f69-152">On the **Montage Online Domain and URLs** section, perform the following steps:</span></span>

    ![Montage Online Domain and URLs single sign-on information](./media/montageonline-tutorial/tutorial_montageonline_url.png)

    <span data-ttu-id="91f69-154">a.</span><span class="sxs-lookup"><span data-stu-id="91f69-154">a.</span></span> <span data-ttu-id="91f69-155">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="91f69-155">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="91f69-156">For Production Environment: `https://<subdomain>.montageonline.co.nz/`</span><span class="sxs-lookup"><span data-stu-id="91f69-156">For Production Environment: `https://<subdomain>.montageonline.co.nz/`</span></span>

    <span data-ttu-id="91f69-157">For Test Environment: `https://build-<subdomain>.montageonline.co.nz/`</span><span class="sxs-lookup"><span data-stu-id="91f69-157">For Test Environment: `https://build-<subdomain>.montageonline.co.nz/`</span></span>

    <span data-ttu-id="91f69-158">b.</span><span class="sxs-lookup"><span data-stu-id="91f69-158">b.</span></span> <span data-ttu-id="91f69-159">In the **Identifier** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="91f69-159">In the **Identifier** textbox, type a URL:</span></span>

    <span data-ttu-id="91f69-160">For Production Environment: `MOL_Azure`</span><span class="sxs-lookup"><span data-stu-id="91f69-160">For Production Environment: `MOL_Azure`</span></span>

    <span data-ttu-id="91f69-161">For Test Environment: `MOL_Azure_Build`</span><span class="sxs-lookup"><span data-stu-id="91f69-161">For Test Environment: `MOL_Azure_Build`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91f69-162">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="91f69-162">The Sign-on URL value is not real.</span></span> <span data-ttu-id="91f69-163">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="91f69-163">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="91f69-164">Contact [Montage Online Client support team](https://www.montage.co.nz/contact-us/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="91f69-164">Contact [Montage Online Client support team](https://www.montage.co.nz/contact-us/) to get the value.</span></span> 
 
1. <span data-ttu-id="91f69-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="91f69-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/montageonline-tutorial/tutorial_montageonline_certificate.png) 

1. <span data-ttu-id="91f69-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="91f69-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/montageonline-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="91f69-169">On the **Montage Online Configuration** section, click **Configure Montage Online** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="91f69-169">On the **Montage Online Configuration** section, click **Configure Montage Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91f69-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="91f69-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Montage Online Configuration](./media/montageonline-tutorial/tutorial_montageonline_configure.png) 

1. <span data-ttu-id="91f69-172">To configure single sign-on on **Montage Online** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Montage Online support team](https://www.montage.co.nz/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="91f69-172">To configure single sign-on on **Montage Online** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Montage Online support team](https://www.montage.co.nz/contact-us/).</span></span> <span data-ttu-id="91f69-173">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="91f69-173">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91f69-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91f69-174">Create an Azure AD test user</span></span>

<span data-ttu-id="91f69-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91f69-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="91f69-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91f69-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91f69-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="91f69-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/montageonline-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="91f69-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="91f69-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/montageonline-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="91f69-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="91f69-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/montageonline-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="91f69-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91f69-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/montageonline-tutorial/create_aaduser_04.png)

    <span data-ttu-id="91f69-186">a.</span><span class="sxs-lookup"><span data-stu-id="91f69-186">a.</span></span> <span data-ttu-id="91f69-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91f69-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91f69-188">b.</span><span class="sxs-lookup"><span data-stu-id="91f69-188">b.</span></span> <span data-ttu-id="91f69-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91f69-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="91f69-190">c.</span><span class="sxs-lookup"><span data-stu-id="91f69-190">c.</span></span> <span data-ttu-id="91f69-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="91f69-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="91f69-192">d.</span><span class="sxs-lookup"><span data-stu-id="91f69-192">d.</span></span> <span data-ttu-id="91f69-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="91f69-193">Click **Create**.</span></span>
 
### <a name="create-a-montage-online-test-user"></a><span data-ttu-id="91f69-194">Create a Montage Online test user</span><span class="sxs-lookup"><span data-stu-id="91f69-194">Create a Montage Online test user</span></span>

<span data-ttu-id="91f69-195">In this section, you create a user called Britta Simon in Montage Online.</span><span class="sxs-lookup"><span data-stu-id="91f69-195">In this section, you create a user called Britta Simon in Montage Online.</span></span> <span data-ttu-id="91f69-196">Work with [Montage Online support team](https://www.montage.co.nz/contact-us/) to add the users in the Montage Online platform.</span><span class="sxs-lookup"><span data-stu-id="91f69-196">Work with [Montage Online support team](https://www.montage.co.nz/contact-us/) to add the users in the Montage Online platform.</span></span> <span data-ttu-id="91f69-197">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="91f69-197">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="91f69-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91f69-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="91f69-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Montage Online.</span><span class="sxs-lookup"><span data-stu-id="91f69-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Montage Online.</span></span>

![Assign the user role][200] 

<span data-ttu-id="91f69-201">**To assign Britta Simon to Montage Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91f69-201">**To assign Britta Simon to Montage Online, perform the following steps:**</span></span>

1. <span data-ttu-id="91f69-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91f69-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="91f69-204">In the applications list, select **Montage Online**.</span><span class="sxs-lookup"><span data-stu-id="91f69-204">In the applications list, select **Montage Online**.</span></span>

    ![The Montage Online link in the Applications list](./media/montageonline-tutorial/tutorial_montageonline_app.png)  

1. <span data-ttu-id="91f69-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="91f69-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="91f69-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="91f69-208">Click **Add** button.</span></span> <span data-ttu-id="91f69-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91f69-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="91f69-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="91f69-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="91f69-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="91f69-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="91f69-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91f69-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="91f69-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="91f69-214">Test single sign-on</span></span>

<span data-ttu-id="91f69-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="91f69-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91f69-216">When you click the Montage Online tile in the Access Panel, you should get automatically signed-on to your Montage Online application.</span><span class="sxs-lookup"><span data-stu-id="91f69-216">When you click the Montage Online tile in the Access Panel, you should get automatically signed-on to your Montage Online application.</span></span>
<span data-ttu-id="91f69-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91f69-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91f69-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="91f69-218">Additional resources</span></span>

* [<span data-ttu-id="91f69-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f69-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="91f69-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91f69-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/montageonline-tutorial/tutorial_general_01.png
[2]: ./media/montageonline-tutorial/tutorial_general_02.png
[3]: ./media/montageonline-tutorial/tutorial_general_03.png
[4]: ./media/montageonline-tutorial/tutorial_general_04.png

[100]: ./media/montageonline-tutorial/tutorial_general_100.png

[200]: ./media/montageonline-tutorial/tutorial_general_200.png
[201]: ./media/montageonline-tutorial/tutorial_general_201.png
[202]: ./media/montageonline-tutorial/tutorial_general_202.png
[203]: ./media/montageonline-tutorial/tutorial_general_203.png

