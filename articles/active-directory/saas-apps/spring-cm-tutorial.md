---
title: 'Tutorial: Azure Active Directory integration with SpringCM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 034d7b61d4a02ac899c7215a042d47bc7938176d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869239"
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="43ca5-103">Tutorial: Azure Active Directory integration with SpringCM</span><span class="sxs-lookup"><span data-stu-id="43ca5-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="43ca5-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43ca5-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43ca5-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="43ca5-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43ca5-106">You can control in Azure AD who has access to SpringCM</span><span class="sxs-lookup"><span data-stu-id="43ca5-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="43ca5-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="43ca5-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43ca5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="43ca5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="43ca5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="43ca5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43ca5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43ca5-110">Prerequisites</span></span>

<span data-ttu-id="43ca5-111">To configure Azure AD integration with SpringCM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="43ca5-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="43ca5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="43ca5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43ca5-113">A SpringCM single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="43ca5-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43ca5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="43ca5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43ca5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="43ca5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43ca5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="43ca5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43ca5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43ca5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43ca5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="43ca5-118">Scenario description</span></span>
<span data-ttu-id="43ca5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="43ca5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43ca5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="43ca5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43ca5-121">Adding SpringCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="43ca5-121">Adding SpringCM from the gallery</span></span>
1. <span data-ttu-id="43ca5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43ca5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="43ca5-123">Adding SpringCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="43ca5-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="43ca5-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="43ca5-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43ca5-125">**To add SpringCM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43ca5-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43ca5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43ca5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="43ca5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43ca5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="43ca5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="43ca5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="43ca5-133">In the search box, type **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-133">In the search box, type **SpringCM**.</span></span>

    ![Creating an Azure AD test user](./media/spring-cm-tutorial/tutorial_springcm_search.png)

1. <span data-ttu-id="43ca5-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="43ca5-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43ca5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43ca5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43ca5-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="43ca5-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43ca5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43ca5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="43ca5-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="43ca5-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="43ca5-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="43ca5-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="43ca5-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="43ca5-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43ca5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="43ca5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="43ca5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43ca5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="43ca5-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="43ca5-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="43ca5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="43ca5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="43ca5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="43ca5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43ca5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43ca5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43ca5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span><span class="sxs-lookup"><span data-stu-id="43ca5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="43ca5-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43ca5-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="43ca5-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="43ca5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="43ca5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_springcm_samlbase.png)

1. <span data-ttu-id="43ca5-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43ca5-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="43ca5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="43ca5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43ca5-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="43ca5-158">This value is not real.</span></span> <span data-ttu-id="43ca5-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="43ca5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="43ca5-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span><span class="sxs-lookup"><span data-stu-id="43ca5-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
1. <span data-ttu-id="43ca5-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="43ca5-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_springcm_certificate.png) 

1. <span data-ttu-id="43ca5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="43ca5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="43ca5-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="43ca5-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="43ca5-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="43ca5-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_springcm_configure.png)     

1. <span data-ttu-id="43ca5-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="43ca5-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

1. <span data-ttu-id="43ca5-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="43ca5-170">![SAML SSO](./media/spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="43ca5-170">![SAML SSO](./media/spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

1. <span data-ttu-id="43ca5-171">In the Identity Provider Configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43ca5-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="43ca5-172">![Identity Provider Configuration](./media/spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span><span class="sxs-lookup"><span data-stu-id="43ca5-172">![Identity Provider Configuration](./media/spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="43ca5-173">a.</span><span class="sxs-lookup"><span data-stu-id="43ca5-173">a.</span></span> <span data-ttu-id="43ca5-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="43ca5-175">b.</span><span class="sxs-lookup"><span data-stu-id="43ca5-175">b.</span></span> <span data-ttu-id="43ca5-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="43ca5-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="43ca5-177">c.</span><span class="sxs-lookup"><span data-stu-id="43ca5-177">c.</span></span> <span data-ttu-id="43ca5-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="43ca5-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="43ca5-179">d.</span><span class="sxs-lookup"><span data-stu-id="43ca5-179">d.</span></span> <span data-ttu-id="43ca5-180">Select **SAML Enabled** as **Enable**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="43ca5-181">e.</span><span class="sxs-lookup"><span data-stu-id="43ca5-181">e.</span></span> <span data-ttu-id="43ca5-182">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="43ca5-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="43ca5-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="43ca5-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="43ca5-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="43ca5-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43ca5-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43ca5-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43ca5-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="43ca5-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43ca5-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="43ca5-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43ca5-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43ca5-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43ca5-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/spring-cm-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="43ca5-192">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/spring-cm-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="43ca5-194">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="43ca5-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/spring-cm-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="43ca5-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43ca5-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43ca5-198">a.</span><span class="sxs-lookup"><span data-stu-id="43ca5-198">a.</span></span> <span data-ttu-id="43ca5-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43ca5-200">b.</span><span class="sxs-lookup"><span data-stu-id="43ca5-200">b.</span></span> <span data-ttu-id="43ca5-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43ca5-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43ca5-202">c.</span><span class="sxs-lookup"><span data-stu-id="43ca5-202">c.</span></span> <span data-ttu-id="43ca5-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43ca5-204">d.</span><span class="sxs-lookup"><span data-stu-id="43ca5-204">d.</span></span> <span data-ttu-id="43ca5-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="43ca5-206">Creating a SpringCM test user</span><span class="sxs-lookup"><span data-stu-id="43ca5-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="43ca5-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span><span class="sxs-lookup"><span data-stu-id="43ca5-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="43ca5-208">In the case of SpringCM, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="43ca5-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="43ca5-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="43ca5-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="43ca5-210">**To provision a user account to SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43ca5-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="43ca5-211">Log in to your **SpringCM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="43ca5-211">Log in to your **SpringCM** company site as administrator.</span></span>

1. <span data-ttu-id="43ca5-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="43ca5-213">![Create User](./media/spring-cm-tutorial/ic797054.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="43ca5-213">![Create User](./media/spring-cm-tutorial/ic797054.png "Create User")</span></span>

1. <span data-ttu-id="43ca5-214">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-214">Click **Create User**.</span></span>

1. <span data-ttu-id="43ca5-215">Select a **User Role**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-215">Select a **User Role**.</span></span>

1. <span data-ttu-id="43ca5-216">Select **Send Activation Email**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-216">Select **Send Activation Email**.</span></span>

1. <span data-ttu-id="43ca5-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="43ca5-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

1. <span data-ttu-id="43ca5-218">Add the user to a **Security group**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-218">Add the user to a **Security group**.</span></span>

1. <span data-ttu-id="43ca5-219">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="43ca5-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="43ca5-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43ca5-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43ca5-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43ca5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span><span class="sxs-lookup"><span data-stu-id="43ca5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Assign User][200] 

<span data-ttu-id="43ca5-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43ca5-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="43ca5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="43ca5-227">In the applications list, select **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-227">In the applications list, select **SpringCM**.</span></span>

    ![Configure Single Sign-On](./media/spring-cm-tutorial/tutorial_springcm_app.png) 

1. <span data-ttu-id="43ca5-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="43ca5-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="43ca5-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="43ca5-231">Click **Add** button.</span></span> <span data-ttu-id="43ca5-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43ca5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="43ca5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="43ca5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="43ca5-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="43ca5-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="43ca5-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43ca5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43ca5-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="43ca5-237">Testing single sign-on</span></span>

<span data-ttu-id="43ca5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="43ca5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="43ca5-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span><span class="sxs-lookup"><span data-stu-id="43ca5-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="43ca5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43ca5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="43ca5-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="43ca5-241">Additional resources</span></span>

* [<span data-ttu-id="43ca5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43ca5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="43ca5-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43ca5-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/spring-cm-tutorial/tutorial_general_203.png

