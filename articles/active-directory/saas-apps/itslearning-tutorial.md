---
title: 'Tutorial: Azure Active Directory integration with itslearning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and itslearning.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: c6fc86d5179a5f7113e955ebc8f6b8994f30cb26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868768"
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="11cbf-103">Tutorial: Azure Active Directory integration with itslearning</span><span class="sxs-lookup"><span data-stu-id="11cbf-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="11cbf-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11cbf-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11cbf-105">Integrating itslearning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="11cbf-105">Integrating itslearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11cbf-106">You can control in Azure AD who has access to itslearning</span><span class="sxs-lookup"><span data-stu-id="11cbf-106">You can control in Azure AD who has access to itslearning</span></span>
- <span data-ttu-id="11cbf-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="11cbf-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11cbf-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="11cbf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="11cbf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="11cbf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11cbf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11cbf-110">Prerequisites</span></span>

<span data-ttu-id="11cbf-111">To configure Azure AD integration with itslearning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="11cbf-111">To configure Azure AD integration with itslearning, you need the following items:</span></span>

- <span data-ttu-id="11cbf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="11cbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11cbf-113">An itslearning single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="11cbf-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11cbf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="11cbf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11cbf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="11cbf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11cbf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="11cbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11cbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11cbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11cbf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="11cbf-118">Scenario description</span></span>
<span data-ttu-id="11cbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="11cbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11cbf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="11cbf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11cbf-121">Adding itslearning from the gallery</span><span class="sxs-lookup"><span data-stu-id="11cbf-121">Adding itslearning from the gallery</span></span>
1. <span data-ttu-id="11cbf-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11cbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-the-gallery"></a><span data-ttu-id="11cbf-123">Adding itslearning from the gallery</span><span class="sxs-lookup"><span data-stu-id="11cbf-123">Adding itslearning from the gallery</span></span>
<span data-ttu-id="11cbf-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="11cbf-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11cbf-125">**To add itslearning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11cbf-125">**To add itslearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11cbf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="11cbf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="11cbf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11cbf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="11cbf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="11cbf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="11cbf-133">In the search box, type **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-133">In the search box, type **itslearning**.</span></span>

    ![Creating an Azure AD test user](./media/itslearning-tutorial/tutorial_itslearning_search.png)

1. <span data-ttu-id="11cbf-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="11cbf-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11cbf-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11cbf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11cbf-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11cbf-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11cbf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11cbf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span></span> <span data-ttu-id="11cbf-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="11cbf-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span></span>

<span data-ttu-id="11cbf-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="11cbf-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11cbf-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="11cbf-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11cbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="11cbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="11cbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11cbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="11cbf-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="11cbf-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="11cbf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11cbf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="11cbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="11cbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11cbf-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11cbf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11cbf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span><span class="sxs-lookup"><span data-stu-id="11cbf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="11cbf-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11cbf-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="11cbf-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="11cbf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11cbf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/itslearning-tutorial/tutorial_itslearning_samlbase.png)

1. <span data-ttu-id="11cbf-155">On the **itslearning Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11cbf-155">On the **itslearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="11cbf-157">a.</span><span class="sxs-lookup"><span data-stu-id="11cbf-157">a.</span></span> <span data-ttu-id="11cbf-158">In the **Sign-on URL** textbox, type a URL as:</span><span class="sxs-lookup"><span data-stu-id="11cbf-158">In the **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="11cbf-159">b.</span><span class="sxs-lookup"><span data-stu-id="11cbf-159">b.</span></span> <span data-ttu-id="11cbf-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="11cbf-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

1. <span data-ttu-id="11cbf-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="11cbf-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/itslearning-tutorial/tutorial_itslearning_certificate.png) 

1. <span data-ttu-id="11cbf-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="11cbf-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/itslearning-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="11cbf-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="11cbf-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="11cbf-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="11cbf-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="11cbf-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="11cbf-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11cbf-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="11cbf-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11cbf-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11cbf-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11cbf-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11cbf-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="11cbf-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11cbf-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="11cbf-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11cbf-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11cbf-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="11cbf-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/itslearning-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="11cbf-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/itslearning-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="11cbf-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="11cbf-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/itslearning-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="11cbf-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11cbf-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11cbf-182">a.</span><span class="sxs-lookup"><span data-stu-id="11cbf-182">a.</span></span> <span data-ttu-id="11cbf-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11cbf-184">b.</span><span class="sxs-lookup"><span data-stu-id="11cbf-184">b.</span></span> <span data-ttu-id="11cbf-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11cbf-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11cbf-186">c.</span><span class="sxs-lookup"><span data-stu-id="11cbf-186">c.</span></span> <span data-ttu-id="11cbf-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11cbf-188">d.</span><span class="sxs-lookup"><span data-stu-id="11cbf-188">d.</span></span> <span data-ttu-id="11cbf-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="11cbf-190">Creating an itslearning test user</span><span class="sxs-lookup"><span data-stu-id="11cbf-190">Creating an itslearning test user</span></span>

<span data-ttu-id="11cbf-191">In this section, you create a user called Britta Simon in itslearning.</span><span class="sxs-lookup"><span data-stu-id="11cbf-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="11cbf-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span><span class="sxs-lookup"><span data-stu-id="11cbf-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span></span> <span data-ttu-id="11cbf-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11cbf-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11cbf-194">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11cbf-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11cbf-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span><span class="sxs-lookup"><span data-stu-id="11cbf-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span></span>

![Assign User][200] 

<span data-ttu-id="11cbf-197">**To assign Britta Simon to itslearning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11cbf-197">**To assign Britta Simon to itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="11cbf-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="11cbf-200">In the applications list, select **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-200">In the applications list, select **itslearning**.</span></span>

    ![Configure Single Sign-On](./media/itslearning-tutorial/tutorial_itslearning_app.png) 

1. <span data-ttu-id="11cbf-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="11cbf-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="11cbf-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="11cbf-204">Click **Add** button.</span></span> <span data-ttu-id="11cbf-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="11cbf-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="11cbf-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="11cbf-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="11cbf-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="11cbf-208">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="11cbf-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="11cbf-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11cbf-210">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="11cbf-210">Testing single sign-on</span></span>

<span data-ttu-id="11cbf-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="11cbf-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11cbf-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span><span class="sxs-lookup"><span data-stu-id="11cbf-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="11cbf-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span><span class="sxs-lookup"><span data-stu-id="11cbf-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span></span>

  ![Login](./media/itslearning-tutorial/login.png)

<span data-ttu-id="11cbf-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11cbf-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11cbf-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="11cbf-216">Additional resources</span></span>

* [<span data-ttu-id="11cbf-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11cbf-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="11cbf-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11cbf-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/itslearning-tutorial/tutorial_general_01.png
[2]: ./media/itslearning-tutorial/tutorial_general_02.png
[3]: ./media/itslearning-tutorial/tutorial_general_03.png
[4]: ./media/itslearning-tutorial/tutorial_general_04.png

[100]: ./media/itslearning-tutorial/tutorial_general_100.png

[200]: ./media/itslearning-tutorial/tutorial_general_200.png
[201]: ./media/itslearning-tutorial/tutorial_general_201.png
[202]: ./media/itslearning-tutorial/tutorial_general_202.png
[203]: ./media/itslearning-tutorial/tutorial_general_203.png

