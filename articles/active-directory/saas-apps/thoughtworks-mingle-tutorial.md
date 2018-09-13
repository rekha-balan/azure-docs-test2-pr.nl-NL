---
title: 'Tutorial: Azure Active Directory integration with Thoughtworks Mingle | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Thoughtworks Mingle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a685b5702aa9f74f3e0abf2a06774a30ac0d996f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869082"
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="46e69-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="46e69-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="46e69-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46e69-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46e69-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="46e69-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46e69-106">You can control in Azure AD who has access to Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="46e69-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="46e69-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="46e69-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46e69-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="46e69-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="46e69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="46e69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46e69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="46e69-110">Prerequisites</span></span>

<span data-ttu-id="46e69-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="46e69-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="46e69-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="46e69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46e69-113">A Thoughtworks Mingle single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="46e69-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46e69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="46e69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46e69-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="46e69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46e69-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="46e69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46e69-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46e69-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46e69-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="46e69-118">Scenario description</span></span>
<span data-ttu-id="46e69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="46e69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46e69-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="46e69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46e69-121">Adding Thoughtworks Mingle from the gallery</span><span class="sxs-lookup"><span data-stu-id="46e69-121">Adding Thoughtworks Mingle from the gallery</span></span>
1. <span data-ttu-id="46e69-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46e69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="46e69-123">Adding Thoughtworks Mingle from the gallery</span><span class="sxs-lookup"><span data-stu-id="46e69-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="46e69-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="46e69-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46e69-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46e69-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46e69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46e69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="46e69-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="46e69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46e69-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46e69-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="46e69-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="46e69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="46e69-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="46e69-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Mingle in the results list](./media/thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="46e69-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46e69-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="46e69-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="46e69-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46e69-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46e69-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="46e69-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span><span class="sxs-lookup"><span data-stu-id="46e69-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="46e69-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="46e69-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="46e69-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="46e69-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46e69-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="46e69-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="46e69-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46e69-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="46e69-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="46e69-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="46e69-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46e69-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="46e69-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="46e69-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="46e69-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46e69-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="46e69-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span><span class="sxs-lookup"><span data-stu-id="46e69-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="46e69-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46e69-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="46e69-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="46e69-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="46e69-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46e69-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

1. <span data-ttu-id="46e69-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46e69-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Thoughtworks Mingle Domain and URLs single sign-on information](./media/thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="46e69-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="46e69-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46e69-156">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="46e69-156">The value is not real.</span></span> <span data-ttu-id="46e69-157">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="46e69-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="46e69-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span><span class="sxs-lookup"><span data-stu-id="46e69-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
1. <span data-ttu-id="46e69-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="46e69-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

1. <span data-ttu-id="46e69-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="46e69-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/thoughtworks-mingle-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="46e69-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="46e69-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

1. <span data-ttu-id="46e69-164">Click the **Admin** tab, and then, click **SSO Config**.</span><span class="sxs-lookup"><span data-stu-id="46e69-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="46e69-165">![Admin tab](./media/thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span><span class="sxs-lookup"><span data-stu-id="46e69-165">![Admin tab](./media/thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

1. <span data-ttu-id="46e69-166">In the **SSO Config** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46e69-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="46e69-167">![SSO Config](./media/thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span><span class="sxs-lookup"><span data-stu-id="46e69-167">![SSO Config](./media/thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="46e69-168">a.</span><span class="sxs-lookup"><span data-stu-id="46e69-168">a.</span></span> <span data-ttu-id="46e69-169">To upload the metadata file, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="46e69-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="46e69-170">b.</span><span class="sxs-lookup"><span data-stu-id="46e69-170">b.</span></span> <span data-ttu-id="46e69-171">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="46e69-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="46e69-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="46e69-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="46e69-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="46e69-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="46e69-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46e69-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="46e69-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46e69-175">Create an Azure AD test user</span></span>
<span data-ttu-id="46e69-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46e69-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="46e69-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46e69-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46e69-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46e69-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/thoughtworks-mingle-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="46e69-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="46e69-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/thoughtworks-mingle-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="46e69-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="46e69-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/thoughtworks-mingle-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="46e69-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46e69-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46e69-187">a.</span><span class="sxs-lookup"><span data-stu-id="46e69-187">a.</span></span> <span data-ttu-id="46e69-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46e69-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46e69-189">b.</span><span class="sxs-lookup"><span data-stu-id="46e69-189">b.</span></span> <span data-ttu-id="46e69-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46e69-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46e69-191">c.</span><span class="sxs-lookup"><span data-stu-id="46e69-191">c.</span></span> <span data-ttu-id="46e69-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="46e69-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46e69-193">d.</span><span class="sxs-lookup"><span data-stu-id="46e69-193">d.</span></span> <span data-ttu-id="46e69-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="46e69-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="46e69-195">Create a Thoughtworks Mingle test user</span><span class="sxs-lookup"><span data-stu-id="46e69-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="46e69-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="46e69-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="46e69-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="46e69-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="46e69-198">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46e69-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="46e69-199">Log in to your Thoughtworks Mingle company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="46e69-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

1. <span data-ttu-id="46e69-200">Click **Profile**.</span><span class="sxs-lookup"><span data-stu-id="46e69-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="46e69-201">![Your First Project](./media/thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span><span class="sxs-lookup"><span data-stu-id="46e69-201">![Your First Project](./media/thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

1. <span data-ttu-id="46e69-202">Click the **Admin** tab, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="46e69-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="46e69-203">![Users](./media/thoughtworks-mingle-tutorial/ic785161.png "Users")</span><span class="sxs-lookup"><span data-stu-id="46e69-203">![Users](./media/thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

1. <span data-ttu-id="46e69-204">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="46e69-204">Click **New User**.</span></span>
   
    <span data-ttu-id="46e69-205">![New User](./media/thoughtworks-mingle-tutorial/ic785162.png "New User")</span><span class="sxs-lookup"><span data-stu-id="46e69-205">![New User](./media/thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

1. <span data-ttu-id="46e69-206">On the **New User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46e69-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="46e69-207">![New User dialog](./media/thoughtworks-mingle-tutorial/ic785163.png "New User")</span><span class="sxs-lookup"><span data-stu-id="46e69-207">![New User dialog](./media/thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="46e69-208">a.</span><span class="sxs-lookup"><span data-stu-id="46e69-208">a.</span></span> <span data-ttu-id="46e69-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="46e69-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="46e69-210">b.</span><span class="sxs-lookup"><span data-stu-id="46e69-210">b.</span></span> <span data-ttu-id="46e69-211">As **User type**, select **Full user**.</span><span class="sxs-lookup"><span data-stu-id="46e69-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="46e69-212">c.</span><span class="sxs-lookup"><span data-stu-id="46e69-212">c.</span></span> <span data-ttu-id="46e69-213">Click **Create This Profile**.</span><span class="sxs-lookup"><span data-stu-id="46e69-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="46e69-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="46e69-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="46e69-215">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46e69-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="46e69-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="46e69-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Assign the user role][200] 

<span data-ttu-id="46e69-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46e69-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="46e69-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46e69-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="46e69-221">In the applications list, select **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="46e69-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![The Thoughtworks Mingle link in the Applications list](./media/thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

1. <span data-ttu-id="46e69-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="46e69-223">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="46e69-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="46e69-225">Click **Add** button.</span></span> <span data-ttu-id="46e69-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46e69-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="46e69-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="46e69-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="46e69-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="46e69-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="46e69-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46e69-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="46e69-231">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="46e69-231">Test single sign-on</span></span>

<span data-ttu-id="46e69-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="46e69-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="46e69-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span><span class="sxs-lookup"><span data-stu-id="46e69-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46e69-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="46e69-234">Additional resources</span></span>

* [<span data-ttu-id="46e69-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46e69-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="46e69-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46e69-236">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/thoughtworks-mingle-tutorial/tutorial_general_203.png

