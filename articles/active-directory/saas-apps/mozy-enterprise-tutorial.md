---
title: 'Tutorial: Azure Active Directory integration with Mozy Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 7dc2f13979bb0ea919a78b750160119198ee7d6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864892"
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="0a990-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="0a990-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="0a990-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a990-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a990-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0a990-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a990-106">You can control in Azure AD who has access to Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="0a990-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="0a990-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0a990-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a990-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0a990-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a990-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0a990-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a990-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a990-110">Prerequisites</span></span>

<span data-ttu-id="0a990-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0a990-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="0a990-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0a990-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a990-113">A Mozy Enterprise single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0a990-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a990-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0a990-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a990-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0a990-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a990-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0a990-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a990-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a990-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a990-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0a990-118">Scenario description</span></span>
<span data-ttu-id="0a990-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0a990-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a990-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a990-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a990-121">Adding Mozy Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a990-121">Adding Mozy Enterprise from the gallery</span></span>
1. <span data-ttu-id="0a990-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a990-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="0a990-123">Adding Mozy Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="0a990-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="0a990-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0a990-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a990-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a990-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a990-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0a990-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0a990-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0a990-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a990-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a990-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0a990-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0a990-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0a990-133">In the search box, type **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="0a990-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

1. <span data-ttu-id="0a990-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0a990-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a990-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a990-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a990-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a990-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a990-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a990-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="0a990-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0a990-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="0a990-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0a990-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a990-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0a990-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a990-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0a990-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0a990-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a990-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0a990-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0a990-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0a990-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a990-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0a990-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0a990-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a990-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a990-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a990-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="0a990-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="0a990-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a990-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="0a990-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0a990-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0a990-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0a990-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

1. <span data-ttu-id="0a990-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a990-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="0a990-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="0a990-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a990-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="0a990-158">This value is not real.</span></span> <span data-ttu-id="0a990-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="0a990-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0a990-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="0a990-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

1. <span data-ttu-id="0a990-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0a990-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

1. <span data-ttu-id="0a990-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0a990-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0a990-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0a990-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a990-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0a990-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

1. <span data-ttu-id="0a990-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0a990-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

1. <span data-ttu-id="0a990-169">In the **Configuration** section, click **Authentication Policy**.</span><span class="sxs-lookup"><span data-stu-id="0a990-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="0a990-170">![Authentication policy](./media/mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span><span class="sxs-lookup"><span data-stu-id="0a990-170">![Authentication policy](./media/mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

1. <span data-ttu-id="0a990-171">On the **Authentication Policy** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a990-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="0a990-172">![Authentication policy](./media/mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span><span class="sxs-lookup"><span data-stu-id="0a990-172">![Authentication policy](./media/mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="0a990-173">a.</span><span class="sxs-lookup"><span data-stu-id="0a990-173">a.</span></span> <span data-ttu-id="0a990-174">Select **Directory Service** as **Provider**.</span><span class="sxs-lookup"><span data-stu-id="0a990-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="0a990-175">b.</span><span class="sxs-lookup"><span data-stu-id="0a990-175">b.</span></span> <span data-ttu-id="0a990-176">Select **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="0a990-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="0a990-177">c.</span><span class="sxs-lookup"><span data-stu-id="0a990-177">c.</span></span> <span data-ttu-id="0a990-178">Click the **SAML Authentication** tab.</span><span class="sxs-lookup"><span data-stu-id="0a990-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="0a990-179">d.</span><span class="sxs-lookup"><span data-stu-id="0a990-179">d.</span></span> <span data-ttu-id="0a990-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0a990-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="0a990-181">e.</span><span class="sxs-lookup"><span data-stu-id="0a990-181">e.</span></span> <span data-ttu-id="0a990-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="0a990-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="0a990-183">f.</span><span class="sxs-lookup"><span data-stu-id="0a990-183">f.</span></span> <span data-ttu-id="0a990-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="0a990-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="0a990-185">g.</span><span class="sxs-lookup"><span data-stu-id="0a990-185">g.</span></span> <span data-ttu-id="0a990-186">Select **Enable SSO for Admins to log in with their network credentials**.</span><span class="sxs-lookup"><span data-stu-id="0a990-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="0a990-187">h.</span><span class="sxs-lookup"><span data-stu-id="0a990-187">h.</span></span> <span data-ttu-id="0a990-188">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="0a990-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0a990-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0a990-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a990-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0a990-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a990-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a990-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a990-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a990-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a990-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a990-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0a990-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a990-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a990-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0a990-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0a990-198">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0a990-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0a990-200">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0a990-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0a990-202">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a990-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a990-204">a.</span><span class="sxs-lookup"><span data-stu-id="0a990-204">a.</span></span> <span data-ttu-id="0a990-205">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a990-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a990-206">b.</span><span class="sxs-lookup"><span data-stu-id="0a990-206">b.</span></span> <span data-ttu-id="0a990-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a990-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a990-208">c.</span><span class="sxs-lookup"><span data-stu-id="0a990-208">c.</span></span> <span data-ttu-id="0a990-209">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0a990-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a990-210">d.</span><span class="sxs-lookup"><span data-stu-id="0a990-210">d.</span></span> <span data-ttu-id="0a990-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a990-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="0a990-212">Creating a Mozy Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="0a990-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="0a990-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0a990-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="0a990-214">In the case of Mozy Enterprise, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="0a990-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="0a990-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0a990-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="0a990-216">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a990-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="0a990-217">Log in to your **Mozy Enterprise** tenant.</span><span class="sxs-lookup"><span data-stu-id="0a990-217">Log in to your **Mozy Enterprise** tenant.</span></span>

1. <span data-ttu-id="0a990-218">Click **Users**, and then click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="0a990-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="0a990-219">![Users](./media/mozy-enterprise-tutorial/ic777317.png "Users")</span><span class="sxs-lookup"><span data-stu-id="0a990-219">![Users](./media/mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="0a990-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span><span class="sxs-lookup"><span data-stu-id="0a990-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="0a990-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span><span class="sxs-lookup"><span data-stu-id="0a990-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
1. <span data-ttu-id="0a990-222">On the new user dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a990-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="0a990-223">![Add Users](./media/mozy-enterprise-tutorial/ic777318.png "Add Users")</span><span class="sxs-lookup"><span data-stu-id="0a990-223">![Add Users](./media/mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="0a990-224">a.</span><span class="sxs-lookup"><span data-stu-id="0a990-224">a.</span></span> <span data-ttu-id="0a990-225">From the **Choose a Group** list, select a group.</span><span class="sxs-lookup"><span data-stu-id="0a990-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="0a990-226">b.</span><span class="sxs-lookup"><span data-stu-id="0a990-226">b.</span></span> <span data-ttu-id="0a990-227">From the **What type of user** list, select a type.</span><span class="sxs-lookup"><span data-stu-id="0a990-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="0a990-228">c.</span><span class="sxs-lookup"><span data-stu-id="0a990-228">c.</span></span> <span data-ttu-id="0a990-229">In the **Username** textbox, type the name of the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="0a990-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="0a990-230">d.</span><span class="sxs-lookup"><span data-stu-id="0a990-230">d.</span></span> <span data-ttu-id="0a990-231">In the **Email** textbox, type the email address of the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="0a990-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="0a990-232">e.</span><span class="sxs-lookup"><span data-stu-id="0a990-232">e.</span></span> <span data-ttu-id="0a990-233">Select **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="0a990-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="0a990-234">f.</span><span class="sxs-lookup"><span data-stu-id="0a990-234">f.</span></span> <span data-ttu-id="0a990-235">Click **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="0a990-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="0a990-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="0a990-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a990-237">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0a990-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a990-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0a990-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Assign User][200] 

<span data-ttu-id="0a990-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0a990-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="0a990-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0a990-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0a990-243">In the applications list, select **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="0a990-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Configure Single Sign-On](./media/mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

1. <span data-ttu-id="0a990-245">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0a990-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0a990-247">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0a990-247">Click **Add** button.</span></span> <span data-ttu-id="0a990-248">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a990-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0a990-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0a990-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0a990-251">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a990-251">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0a990-252">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0a990-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a990-253">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a990-253">Testing single sign-on</span></span>

<span data-ttu-id="0a990-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0a990-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a990-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="0a990-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="0a990-256">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a990-256">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a990-257">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0a990-257">Additional resources</span></span>

* [<span data-ttu-id="0a990-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a990-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0a990-259">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a990-259">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/mozy-enterprise-tutorial/tutorial_general_203.png

