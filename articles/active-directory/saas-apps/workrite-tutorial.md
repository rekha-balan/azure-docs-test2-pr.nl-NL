---
title: 'Tutorial: Azure Active Directory integration with Workrite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workrite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: dd6a58656d91ff8dacbba36050198cba19f4d1e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966025"
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="dab46-103">Tutorial: Azure Active Directory integration with Workrite</span><span class="sxs-lookup"><span data-stu-id="dab46-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="dab46-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dab46-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dab46-105">Integrating Workrite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dab46-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dab46-106">You can control in Azure AD who has access to Workrite.</span><span class="sxs-lookup"><span data-stu-id="dab46-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="dab46-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dab46-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dab46-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dab46-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dab46-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dab46-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab46-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dab46-110">Prerequisites</span></span>

<span data-ttu-id="dab46-111">To configure Azure AD integration with Workrite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dab46-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="dab46-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dab46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dab46-113">A Workrite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dab46-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dab46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dab46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dab46-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dab46-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dab46-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dab46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dab46-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dab46-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dab46-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dab46-118">Scenario description</span></span>
<span data-ttu-id="dab46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dab46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dab46-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dab46-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dab46-121">Adding Workrite from the gallery</span><span class="sxs-lookup"><span data-stu-id="dab46-121">Adding Workrite from the gallery</span></span>
1. <span data-ttu-id="dab46-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="dab46-123">Adding Workrite from the gallery</span><span class="sxs-lookup"><span data-stu-id="dab46-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="dab46-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dab46-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dab46-125">**To add Workrite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab46-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dab46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dab46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="dab46-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dab46-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dab46-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dab46-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="dab46-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dab46-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="dab46-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dab46-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite in the results list](./media/workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dab46-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab46-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dab46-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dab46-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dab46-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dab46-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="dab46-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dab46-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="dab46-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="dab46-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dab46-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dab46-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dab46-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dab46-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dab46-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab46-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dab46-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dab46-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="dab46-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dab46-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dab46-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dab46-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dab46-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab46-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dab46-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span><span class="sxs-lookup"><span data-stu-id="dab46-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="dab46-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab46-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="dab46-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dab46-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="dab46-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dab46-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/workrite-tutorial/tutorial_workrite_samlbase.png)

1. <span data-ttu-id="dab46-153">On the **Workrite Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dab46-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Workrite Domain and URLs single sign-on information](./media/workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="dab46-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="dab46-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dab46-156">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="dab46-156">This value is not real.</span></span> <span data-ttu-id="dab46-157">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="dab46-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="dab46-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span><span class="sxs-lookup"><span data-stu-id="dab46-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

1. <span data-ttu-id="dab46-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dab46-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/workrite-tutorial/tutorial_workrite_certificate.png) 

1. <span data-ttu-id="dab46-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dab46-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/workrite-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="dab46-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dab46-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dab46-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="dab46-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Workrite Configuration](./media/workrite-tutorial/tutorial_workrite_configure.png) 

1. <span data-ttu-id="dab46-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="dab46-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="dab46-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dab46-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dab46-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dab46-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dab46-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dab46-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dab46-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dab46-170">Create an Azure AD test user</span></span>

<span data-ttu-id="dab46-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab46-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="dab46-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab46-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dab46-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="dab46-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/workrite-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="dab46-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dab46-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/workrite-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="dab46-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dab46-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/workrite-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="dab46-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dab46-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dab46-182">a.</span><span class="sxs-lookup"><span data-stu-id="dab46-182">a.</span></span> <span data-ttu-id="dab46-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dab46-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dab46-184">b.</span><span class="sxs-lookup"><span data-stu-id="dab46-184">b.</span></span> <span data-ttu-id="dab46-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dab46-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dab46-186">c.</span><span class="sxs-lookup"><span data-stu-id="dab46-186">c.</span></span> <span data-ttu-id="dab46-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="dab46-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dab46-188">d.</span><span class="sxs-lookup"><span data-stu-id="dab46-188">d.</span></span> <span data-ttu-id="dab46-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dab46-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="dab46-190">Create a Workrite test user</span><span class="sxs-lookup"><span data-stu-id="dab46-190">Create a Workrite test user</span></span>

<span data-ttu-id="dab46-191">The objective of this section is to create a user called Britta Simon in Workrite.</span><span class="sxs-lookup"><span data-stu-id="dab46-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="dab46-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab46-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="dab46-193">Sign on to your workrite company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="dab46-193">Sign on to your workrite company site as administrator.</span></span>

1. <span data-ttu-id="dab46-194">In the navigation pane, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="dab46-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Admin Control][400]

1. <span data-ttu-id="dab46-196">Go to Quick Links, and then click **Create a User**.</span><span class="sxs-lookup"><span data-stu-id="dab46-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Create User Section][401]

1. <span data-ttu-id="dab46-198">On the **Create User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dab46-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Create User Dailog][402]
    
    <span data-ttu-id="dab46-200">a.</span><span class="sxs-lookup"><span data-stu-id="dab46-200">a.</span></span> <span data-ttu-id="dab46-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="dab46-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="dab46-202">b.</span><span class="sxs-lookup"><span data-stu-id="dab46-202">b.</span></span> <span data-ttu-id="dab46-203">In the **First Name** textbox, type the firstname of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="dab46-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="dab46-204">c.</span><span class="sxs-lookup"><span data-stu-id="dab46-204">c.</span></span> <span data-ttu-id="dab46-205">In the **Surname** textbox, type the surname of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="dab46-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="dab46-206">d.</span><span class="sxs-lookup"><span data-stu-id="dab46-206">d.</span></span> <span data-ttu-id="dab46-207">Select **Client Administrator** as **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="dab46-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="dab46-208">e.</span><span class="sxs-lookup"><span data-stu-id="dab46-208">e.</span></span> <span data-ttu-id="dab46-209">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dab46-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dab46-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dab46-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="dab46-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span><span class="sxs-lookup"><span data-stu-id="dab46-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Assign the user role][200] 

<span data-ttu-id="dab46-213">**To assign Britta Simon to Workrite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dab46-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="dab46-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dab46-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="dab46-216">In the applications list, select **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="dab46-216">In the applications list, select **Workrite**.</span></span>

    ![The Workrite link in the Applications list](./media/workrite-tutorial/tutorial_workrite_app.png)  

1. <span data-ttu-id="dab46-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dab46-218">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="dab46-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dab46-220">Click **Add** button.</span></span> <span data-ttu-id="dab46-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab46-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="dab46-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dab46-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="dab46-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab46-224">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="dab46-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dab46-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dab46-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dab46-226">Test single sign-on</span></span>

<span data-ttu-id="dab46-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dab46-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="dab46-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span><span class="sxs-lookup"><span data-stu-id="dab46-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dab46-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dab46-229">Additional resources</span></span>

* [<span data-ttu-id="dab46-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dab46-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dab46-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dab46-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/workrite-tutorial/tutorial_general_01.png
[2]: ./media/workrite-tutorial/tutorial_general_02.png
[3]: ./media/workrite-tutorial/tutorial_general_03.png
[4]: ./media/workrite-tutorial/tutorial_general_04.png

[100]: ./media/workrite-tutorial/tutorial_general_100.png

[200]: ./media/workrite-tutorial/tutorial_general_200.png
[201]: ./media/workrite-tutorial/tutorial_general_201.png
[202]: ./media/workrite-tutorial/tutorial_general_202.png
[203]: ./media/workrite-tutorial/tutorial_general_203.png
[400]: ./media/workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/workrite-tutorial/tutorial_workrite_402.png

