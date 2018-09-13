---
title: 'Tutorial: Azure Active Directory integration with Halosys | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Halosys.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2018
ms.author: jeedes
ms.openlocfilehash: 6e0b9d205bf16c92443aadc69a1186b99c6d8cc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866726"
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="18902-103">Tutorial: Azure Active Directory integration with Halosys</span><span class="sxs-lookup"><span data-stu-id="18902-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="18902-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18902-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18902-105">Integrating Halosys with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="18902-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18902-106">You can control in Azure AD who has access to Halosys.</span><span class="sxs-lookup"><span data-stu-id="18902-106">You can control in Azure AD who has access to Halosys.</span></span>
- <span data-ttu-id="18902-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="18902-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="18902-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="18902-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="18902-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="18902-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18902-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="18902-110">Prerequisites</span></span>

<span data-ttu-id="18902-111">To configure Azure AD integration with Halosys, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="18902-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="18902-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="18902-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18902-113">A Halosys single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="18902-113">A Halosys single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18902-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="18902-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18902-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="18902-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18902-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="18902-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18902-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18902-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18902-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="18902-118">Scenario description</span></span>
<span data-ttu-id="18902-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="18902-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18902-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="18902-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18902-121">Adding Halosys from the gallery</span><span class="sxs-lookup"><span data-stu-id="18902-121">Adding Halosys from the gallery</span></span>
1. <span data-ttu-id="18902-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="18902-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="18902-123">Adding Halosys from the gallery</span><span class="sxs-lookup"><span data-stu-id="18902-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="18902-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="18902-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18902-125">**To add Halosys from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="18902-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18902-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="18902-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="18902-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="18902-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18902-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="18902-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="18902-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="18902-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="18902-133">In the search box, type **Halosys**, select **Halosys** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="18902-133">In the search box, type **Halosys**, select **Halosys** from result panel then click **Add** button to add the application.</span></span>

    ![Halosys in the results list](./media/halosys-tutorial/tutorial_halosys_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18902-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="18902-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="18902-136">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="18902-136">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18902-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18902-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="18902-138">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span><span class="sxs-lookup"><span data-stu-id="18902-138">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="18902-139">In Halosys, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="18902-139">In Halosys, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18902-140">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="18902-140">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18902-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="18902-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="18902-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18902-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="18902-143">**[Create a Halosys test user](#create-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="18902-143">**[Create a Halosys test user](#create-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="18902-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="18902-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="18902-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="18902-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="18902-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="18902-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="18902-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halosys application.</span><span class="sxs-lookup"><span data-stu-id="18902-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halosys application.</span></span>

<span data-ttu-id="18902-148">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="18902-148">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="18902-149">In the Azure portal, on the **Halosys** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="18902-149">In the Azure portal, on the **Halosys** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="18902-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="18902-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/halosys-tutorial/tutorial_halosys_samlbase.png)

1. <span data-ttu-id="18902-153">On the **Halosys Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="18902-153">On the **Halosys Domain and URLs** section, perform the following steps:</span></span>

    ![Halosys Domain and URLs single sign-on information](./media/halosys-tutorial/tutorial_halosys_url.png)

    <span data-ttu-id="18902-155">a.</span><span class="sxs-lookup"><span data-stu-id="18902-155">a.</span></span> <span data-ttu-id="18902-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.halosys.com`</span><span class="sxs-lookup"><span data-stu-id="18902-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.halosys.com`</span></span>

    <span data-ttu-id="18902-157">b.</span><span class="sxs-lookup"><span data-stu-id="18902-157">b.</span></span> <span data-ttu-id="18902-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.halosys.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="18902-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.halosys.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18902-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="18902-159">These values are not real.</span></span> <span data-ttu-id="18902-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="18902-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="18902-161">Contact [Halosys support team](http://halosys.com/halosys#contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="18902-161">Contact [Halosys support team](http://halosys.com/halosys#contact) to get these values.</span></span>
 
1. <span data-ttu-id="18902-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="18902-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/halosys-tutorial/tutorial_halosys_certificate.png) 

1. <span data-ttu-id="18902-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="18902-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/halosys-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="18902-166">On the **Halosys Configuration** section, click **Configure Halosys** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="18902-166">On the **Halosys Configuration** section, click **Configure Halosys** to open **Configure sign-on** window.</span></span> <span data-ttu-id="18902-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="18902-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Halosys Configuration](./media/halosys-tutorial/tutorial_halosys_configure.png) 

1. <span data-ttu-id="18902-169">To configure single sign-on on **Halosys** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Halosys support team](http://halosys.com/halosys#contact).</span><span class="sxs-lookup"><span data-stu-id="18902-169">To configure single sign-on on **Halosys** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Halosys support team](http://halosys.com/halosys#contact).</span></span> <span data-ttu-id="18902-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="18902-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="18902-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="18902-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18902-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="18902-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18902-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18902-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18902-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="18902-174">Create an Azure AD test user</span></span>

<span data-ttu-id="18902-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18902-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="18902-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="18902-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18902-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="18902-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/halosys-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="18902-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="18902-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/halosys-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="18902-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="18902-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/halosys-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="18902-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="18902-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/halosys-tutorial/create_aaduser_04.png)

    <span data-ttu-id="18902-186">a.</span><span class="sxs-lookup"><span data-stu-id="18902-186">a.</span></span> <span data-ttu-id="18902-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18902-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18902-188">b.</span><span class="sxs-lookup"><span data-stu-id="18902-188">b.</span></span> <span data-ttu-id="18902-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18902-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="18902-190">c.</span><span class="sxs-lookup"><span data-stu-id="18902-190">c.</span></span> <span data-ttu-id="18902-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="18902-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="18902-192">d.</span><span class="sxs-lookup"><span data-stu-id="18902-192">d.</span></span> <span data-ttu-id="18902-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="18902-193">Click **Create**.</span></span>
  
### <a name="create-a-halosys-test-user"></a><span data-ttu-id="18902-194">Create a Halosys test user</span><span class="sxs-lookup"><span data-stu-id="18902-194">Create a Halosys test user</span></span>

<span data-ttu-id="18902-195">In this section, you create a user called Britta Simon in Halosys.</span><span class="sxs-lookup"><span data-stu-id="18902-195">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="18902-196">Work with [Halosys support team](http://halosys.com/halosys#contact) to add the users in the Halosys platform.</span><span class="sxs-lookup"><span data-stu-id="18902-196">Work with [Halosys support team](http://halosys.com/halosys#contact) to add the users in the Halosys platform.</span></span> <span data-ttu-id="18902-197">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="18902-197">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="18902-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="18902-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="18902-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halosys.</span><span class="sxs-lookup"><span data-stu-id="18902-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halosys.</span></span>

![Assign the user role][200] 

<span data-ttu-id="18902-201">**To assign Britta Simon to Halosys, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="18902-201">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="18902-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="18902-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="18902-204">In the applications list, select **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="18902-204">In the applications list, select **Halosys**.</span></span>

    ![The Halosys link in the Applications list](./media/halosys-tutorial/tutorial_halosys_app.png)  

1. <span data-ttu-id="18902-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="18902-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="18902-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="18902-208">Click **Add** button.</span></span> <span data-ttu-id="18902-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="18902-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="18902-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="18902-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="18902-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="18902-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="18902-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="18902-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="18902-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="18902-214">Test single sign-on</span></span>

<span data-ttu-id="18902-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="18902-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18902-216">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span><span class="sxs-lookup"><span data-stu-id="18902-216">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>
<span data-ttu-id="18902-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18902-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="18902-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="18902-218">Additional resources</span></span>

* [<span data-ttu-id="18902-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18902-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="18902-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18902-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/halosys-tutorial/tutorial_general_01.png
[2]: ./media/halosys-tutorial/tutorial_general_02.png
[3]: ./media/halosys-tutorial/tutorial_general_03.png
[4]: ./media/halosys-tutorial/tutorial_general_04.png

[100]: ./media/halosys-tutorial/tutorial_general_100.png

[200]: ./media/halosys-tutorial/tutorial_general_200.png
[201]: ./media/halosys-tutorial/tutorial_general_201.png
[202]: ./media/halosys-tutorial/tutorial_general_202.png
[203]: ./media/halosys-tutorial/tutorial_general_203.png

