---
title: 'Tutorial: Azure Active Directory integration with Flatter Files | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Flatter Files.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: b0660e14b858cc77026ea008fcf122c79e656c13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866271"
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="1b10a-103">Tutorial: Azure Active Directory integration with Flatter Files</span><span class="sxs-lookup"><span data-stu-id="1b10a-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="1b10a-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b10a-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b10a-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1b10a-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b10a-106">You can control in Azure AD who has access to Flatter Files</span><span class="sxs-lookup"><span data-stu-id="1b10a-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="1b10a-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1b10a-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b10a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1b10a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1b10a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1b10a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b10a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b10a-110">Prerequisites</span></span>

<span data-ttu-id="1b10a-111">To configure Azure AD integration with Flatter Files, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1b10a-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="1b10a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1b10a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b10a-113">A Flatter Files single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1b10a-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b10a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1b10a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b10a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1b10a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b10a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1b10a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b10a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b10a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b10a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1b10a-118">Scenario description</span></span>
<span data-ttu-id="1b10a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1b10a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b10a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b10a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b10a-121">Adding Flatter Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b10a-121">Adding Flatter Files from the gallery</span></span>
1. <span data-ttu-id="1b10a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b10a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="1b10a-123">Adding Flatter Files from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b10a-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="1b10a-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1b10a-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b10a-125">**To add Flatter Files from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b10a-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b10a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1b10a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="1b10a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b10a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="1b10a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1b10a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="1b10a-133">In the search box, type **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-133">In the search box, type **Flatter Files**.</span></span>

    ![Creating an Azure AD test user](./media/flatter-files-tutorial/tutorial_flatterfiles_search.png)

1. <span data-ttu-id="1b10a-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1b10a-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b10a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b10a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b10a-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b10a-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b10a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b10a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="1b10a-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1b10a-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="1b10a-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1b10a-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1b10a-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b10a-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b10a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1b10a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1b10a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b10a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1b10a-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1b10a-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1b10a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b10a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1b10a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1b10a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b10a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b10a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b10a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span><span class="sxs-lookup"><span data-stu-id="1b10a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="1b10a-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b10a-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1b10a-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="1b10a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b10a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

1. <span data-ttu-id="1b10a-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="1b10a-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
1. <span data-ttu-id="1b10a-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b10a-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

1. <span data-ttu-id="1b10a-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1b10a-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1b10a-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1b10a-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1b10a-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1b10a-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

1. <span data-ttu-id="1b10a-164">Sign-on to your Flatter Files application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1b10a-164">Sign-on to your Flatter Files application as an administrator.</span></span>

1. <span data-ttu-id="1b10a-165">Click **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-165">Click **DASHBOARD**.</span></span> 
   
    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatter_files_05.png)  

1. <span data-ttu-id="1b10a-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span><span class="sxs-lookup"><span data-stu-id="1b10a-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="1b10a-169">a.</span><span class="sxs-lookup"><span data-stu-id="1b10a-169">a.</span></span> <span data-ttu-id="1b10a-170">Select **Use SAML 2.0 for Authentication**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="1b10a-171">b.</span><span class="sxs-lookup"><span data-stu-id="1b10a-171">b.</span></span> <span data-ttu-id="1b10a-172">Click **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-172">Click **Configure SAML**.</span></span>

1. <span data-ttu-id="1b10a-173">On the **SAML Configuration** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b10a-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="1b10a-175">a.</span><span class="sxs-lookup"><span data-stu-id="1b10a-175">a.</span></span> <span data-ttu-id="1b10a-176">In the **Domain** textbox, type your registered domain.</span><span class="sxs-lookup"><span data-stu-id="1b10a-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1b10a-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="1b10a-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="1b10a-178">b.</span><span class="sxs-lookup"><span data-stu-id="1b10a-178">b.</span></span> <span data-ttu-id="1b10a-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b10a-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="1b10a-180">c.</span><span class="sxs-lookup"><span data-stu-id="1b10a-180">c.</span></span>  <span data-ttu-id="1b10a-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="1b10a-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="1b10a-182">d.</span><span class="sxs-lookup"><span data-stu-id="1b10a-182">d.</span></span> <span data-ttu-id="1b10a-183">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="1b10a-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1b10a-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1b10a-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1b10a-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1b10a-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b10a-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b10a-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b10a-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b10a-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b10a-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="1b10a-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b10a-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b10a-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1b10a-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/flatter-files-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="1b10a-193">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/flatter-files-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="1b10a-195">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1b10a-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/flatter-files-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="1b10a-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b10a-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b10a-199">a.</span><span class="sxs-lookup"><span data-stu-id="1b10a-199">a.</span></span> <span data-ttu-id="1b10a-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b10a-201">b.</span><span class="sxs-lookup"><span data-stu-id="1b10a-201">b.</span></span> <span data-ttu-id="1b10a-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b10a-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b10a-203">c.</span><span class="sxs-lookup"><span data-stu-id="1b10a-203">c.</span></span> <span data-ttu-id="1b10a-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1b10a-205">d.</span><span class="sxs-lookup"><span data-stu-id="1b10a-205">d.</span></span> <span data-ttu-id="1b10a-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="1b10a-207">Creating a Flatter Files test user</span><span class="sxs-lookup"><span data-stu-id="1b10a-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="1b10a-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="1b10a-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="1b10a-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b10a-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1b10a-210">Sign on to your **Flatter Files** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="1b10a-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

1. <span data-ttu-id="1b10a-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="1b10a-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Create a Flatter Files User](./media/flatter-files-tutorial/tutorial_flatter_files_09.png)

1. <span data-ttu-id="1b10a-213">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-213">Click **Add User**.</span></span> 

1. <span data-ttu-id="1b10a-214">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b10a-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Create a Flatter Files User](./media/flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="1b10a-216">a.</span><span class="sxs-lookup"><span data-stu-id="1b10a-216">a.</span></span> <span data-ttu-id="1b10a-217">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="1b10a-218">b.</span><span class="sxs-lookup"><span data-stu-id="1b10a-218">b.</span></span> <span data-ttu-id="1b10a-219">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="1b10a-220">c.</span><span class="sxs-lookup"><span data-stu-id="1b10a-220">c.</span></span> <span data-ttu-id="1b10a-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b10a-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="1b10a-222">d.</span><span class="sxs-lookup"><span data-stu-id="1b10a-222">d.</span></span> <span data-ttu-id="1b10a-223">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b10a-224">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b10a-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1b10a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="1b10a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Assign User][200] 

<span data-ttu-id="1b10a-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b10a-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1b10a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1b10a-230">In the applications list, select **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-230">In the applications list, select **Flatter Files**.</span></span>

    ![Configure Single Sign-On](./media/flatter-files-tutorial/tutorial_flatterfiles_app.png) 

1. <span data-ttu-id="1b10a-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1b10a-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="1b10a-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1b10a-234">Click **Add** button.</span></span> <span data-ttu-id="1b10a-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b10a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="1b10a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1b10a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1b10a-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b10a-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1b10a-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b10a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b10a-240">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b10a-240">Testing single sign-on</span></span>

<span data-ttu-id="1b10a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1b10a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b10a-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span><span class="sxs-lookup"><span data-stu-id="1b10a-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="1b10a-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b10a-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b10a-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1b10a-244">Additional resources</span></span>

* [<span data-ttu-id="1b10a-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b10a-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1b10a-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b10a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/flatter-files-tutorial/tutorial_general_203.png

