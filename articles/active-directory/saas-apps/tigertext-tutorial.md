---
title: 'Tutorial: Azure Active Directory integration with TigerText Secure Messenger | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TigerText Secure Messenger.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e74a1a17638a3d968f2216950f6310205fce86f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868350"
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="4bdb0-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="4bdb0-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="4bdb0-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bdb0-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bdb0-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4bdb0-106">You can control in Azure AD who has access to TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="4bdb0-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="4bdb0-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4bdb0-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bdb0-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4bdb0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4bdb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4bdb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bdb0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4bdb0-110">Prerequisites</span></span>

<span data-ttu-id="4bdb0-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="4bdb0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4bdb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bdb0-113">A TigerText Secure Messenger single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4bdb0-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bdb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bdb0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bdb0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bdb0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bdb0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bdb0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4bdb0-118">Scenario description</span></span>
<span data-ttu-id="4bdb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bdb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bdb0-121">Add TigerText Secure Messenger from the gallery</span><span class="sxs-lookup"><span data-stu-id="4bdb0-121">Add TigerText Secure Messenger from the gallery</span></span>
1. <span data-ttu-id="4bdb0-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bdb0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="4bdb0-123">Add TigerText Secure Messenger from the gallery</span><span class="sxs-lookup"><span data-stu-id="4bdb0-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="4bdb0-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4bdb0-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bdb0-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4bdb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4bdb0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4bdb0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4bdb0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4bdb0-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Add from gallery](./media/tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4bdb0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bdb0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4bdb0-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4bdb0-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bdb0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="4bdb0-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="4bdb0-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4bdb0-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4bdb0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4bdb0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4bdb0-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4bdb0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4bdb0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4bdb0-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bdb0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4bdb0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="4bdb0-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bdb0-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="4bdb0-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4bdb0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML-based Sign-on](./media/tigertext-tutorial/tutorial_tigertext_samlbase.png)

1. <span data-ttu-id="4bdb0-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![TigerText Secure Messenger Domain and URLs section](./media/tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="4bdb0-155">a.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-155">a.</span></span> <span data-ttu-id="4bdb0-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="4bdb0-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="4bdb0-157">b.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-157">b.</span></span> <span data-ttu-id="4bdb0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="4bdb0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bdb0-159">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-159">This value is not real.</span></span> <span data-ttu-id="4bdb0-160">Update this value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="4bdb0-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
1. <span data-ttu-id="4bdb0-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/tigertext-tutorial/tutorial_tigertext_certificate.png) 

1. <span data-ttu-id="4bdb0-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-164">Click **Save** button.</span></span>

    ![Save Button](./media/tigertext-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4bdb0-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="4bdb0-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4bdb0-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4bdb0-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4bdb0-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4bdb0-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4bdb0-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4bdb0-170">Create an Azure AD test user</span></span>
<span data-ttu-id="4bdb0-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4bdb0-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bdb0-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4bdb0-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tigertext-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4bdb0-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Users and groups->All users](./media/tigertext-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4bdb0-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add Button](./media/tigertext-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4bdb0-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4bdb0-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![User dialog](./media/tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bdb0-182">a.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-182">a.</span></span> <span data-ttu-id="4bdb0-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bdb0-184">b.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-184">b.</span></span> <span data-ttu-id="4bdb0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bdb0-186">c.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-186">c.</span></span> <span data-ttu-id="4bdb0-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4bdb0-188">d.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-188">d.</span></span> <span data-ttu-id="4bdb0-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="4bdb0-190">Create a TigerText Secure Messenger test user</span><span class="sxs-lookup"><span data-stu-id="4bdb0-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="4bdb0-191">In this section, you create a user called Britta Simon in TigerText.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="4bdb0-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4bdb0-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4bdb0-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="4bdb0-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Assign User][200] 

<span data-ttu-id="4bdb0-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4bdb0-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="4bdb0-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4bdb0-199">In the applications list, select **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger in app list](./media/tigertext-tutorial/tutorial_tigertext_app.png) 

1. <span data-ttu-id="4bdb0-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4bdb0-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-203">Click **Add** button.</span></span> <span data-ttu-id="4bdb0-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4bdb0-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4bdb0-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4bdb0-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4bdb0-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4bdb0-209">Test single sign-on</span></span>

<span data-ttu-id="4bdb0-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4bdb0-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span><span class="sxs-lookup"><span data-stu-id="4bdb0-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="4bdb0-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4bdb0-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bdb0-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4bdb0-213">Additional resources</span></span>

* [<span data-ttu-id="4bdb0-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bdb0-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4bdb0-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4bdb0-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tigertext-tutorial/tutorial_general_01.png
[2]: ./media/tigertext-tutorial/tutorial_general_02.png
[3]: ./media/tigertext-tutorial/tutorial_general_03.png
[4]: ./media/tigertext-tutorial/tutorial_general_04.png

[100]: ./media/tigertext-tutorial/tutorial_general_100.png

[200]: ./media/tigertext-tutorial/tutorial_general_200.png
[201]: ./media/tigertext-tutorial/tutorial_general_201.png
[202]: ./media/tigertext-tutorial/tutorial_general_202.png
[203]: ./media/tigertext-tutorial/tutorial_general_203.png

