---
title: 'Tutorial: Azure Active Directory integration with ClickTime | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ClickTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 065225bb6c206f980c19955c682fc2c8a5deb950
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968843"
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="f0763-103">Tutorial: Azure Active Directory integration with ClickTime</span><span class="sxs-lookup"><span data-stu-id="f0763-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="f0763-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0763-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0763-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f0763-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0763-106">You can control in Azure AD who has access to ClickTime</span><span class="sxs-lookup"><span data-stu-id="f0763-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="f0763-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f0763-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0763-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f0763-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0763-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f0763-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0763-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0763-110">Prerequisites</span></span>

<span data-ttu-id="f0763-111">To configure Azure AD integration with ClickTime, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f0763-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="f0763-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f0763-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0763-113">A ClickTime single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f0763-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0763-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f0763-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0763-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f0763-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0763-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f0763-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0763-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0763-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0763-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f0763-118">Scenario description</span></span>
<span data-ttu-id="f0763-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f0763-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0763-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0763-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0763-121">Adding ClickTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0763-121">Adding ClickTime from the gallery</span></span>
1. <span data-ttu-id="f0763-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0763-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="f0763-123">Adding ClickTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0763-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="f0763-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f0763-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0763-125">**To add ClickTime from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0763-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0763-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f0763-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="f0763-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f0763-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0763-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0763-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="f0763-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f0763-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="f0763-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f0763-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime in the results list](./media/clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f0763-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0763-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f0763-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f0763-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0763-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0763-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="f0763-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f0763-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="f0763-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f0763-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0763-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0763-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0763-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f0763-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f0763-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0763-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f0763-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f0763-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f0763-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0763-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f0763-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f0763-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f0763-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0763-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f0763-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span><span class="sxs-lookup"><span data-stu-id="f0763-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="f0763-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0763-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f0763-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f0763-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="f0763-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0763-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/clicktime-tutorial/tutorial_clicktime_samlbase.png)

1. <span data-ttu-id="f0763-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0763-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![ClickTime Domain and URLs single sign-on information](./media/clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="f0763-155">a.</span><span class="sxs-lookup"><span data-stu-id="f0763-155">a.</span></span> <span data-ttu-id="f0763-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="f0763-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="f0763-157">b.</span><span class="sxs-lookup"><span data-stu-id="f0763-157">b.</span></span> <span data-ttu-id="f0763-158">In the **Reply URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="f0763-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

1. <span data-ttu-id="f0763-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f0763-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/clicktime-tutorial/tutorial_clicktime_certificate.png) 

1. <span data-ttu-id="f0763-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f0763-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/clicktime-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f0763-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f0763-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0763-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f0763-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ClickTime configuration](./media/clicktime-tutorial/tutorial_clicktime_configure.png) 

1. <span data-ttu-id="f0763-166">In a different web browser window, log into your ClickTime company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f0763-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

1. <span data-ttu-id="f0763-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span><span class="sxs-lookup"><span data-stu-id="f0763-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

1. <span data-ttu-id="f0763-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0763-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="f0763-169">![Security Settings](./media/clicktime-tutorial/tic777280.png "Security Settings")</span><span class="sxs-lookup"><span data-stu-id="f0763-169">![Security Settings](./media/clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="f0763-170">a.</span><span class="sxs-lookup"><span data-stu-id="f0763-170">a.</span></span>  <span data-ttu-id="f0763-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="f0763-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="f0763-172">b.</span><span class="sxs-lookup"><span data-stu-id="f0763-172">b.</span></span> <span data-ttu-id="f0763-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f0763-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f0763-174">c.</span><span class="sxs-lookup"><span data-stu-id="f0763-174">c.</span></span>  <span data-ttu-id="f0763-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="f0763-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="f0763-176">d.</span><span class="sxs-lookup"><span data-stu-id="f0763-176">d.</span></span>  <span data-ttu-id="f0763-177">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f0763-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f0763-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f0763-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0763-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f0763-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0763-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0763-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f0763-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0763-181">Create an Azure AD test user</span></span>
<span data-ttu-id="f0763-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0763-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="f0763-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0763-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0763-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f0763-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/clicktime-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f0763-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f0763-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/clicktime-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f0763-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f0763-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![The Add button](./media/clicktime-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f0763-191">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0763-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![The User dialog box](./media/clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0763-193">a.</span><span class="sxs-lookup"><span data-stu-id="f0763-193">a.</span></span> <span data-ttu-id="f0763-194">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0763-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0763-195">b.</span><span class="sxs-lookup"><span data-stu-id="f0763-195">b.</span></span> <span data-ttu-id="f0763-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0763-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0763-197">c.</span><span class="sxs-lookup"><span data-stu-id="f0763-197">c.</span></span> <span data-ttu-id="f0763-198">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f0763-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0763-199">d.</span><span class="sxs-lookup"><span data-stu-id="f0763-199">d.</span></span> <span data-ttu-id="f0763-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0763-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="f0763-201">Create a ClickTime test user</span><span class="sxs-lookup"><span data-stu-id="f0763-201">Create a ClickTime test user</span></span>

<span data-ttu-id="f0763-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span><span class="sxs-lookup"><span data-stu-id="f0763-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="f0763-203">In the case of ClickTime, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f0763-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="f0763-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f0763-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="f0763-205">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0763-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="f0763-206">Log in to your **ClickTime** tenant.</span><span class="sxs-lookup"><span data-stu-id="f0763-206">Log in to your **ClickTime** tenant.</span></span>
1. <span data-ttu-id="f0763-207">In the toolbar on the top, click **Company**, and then click **People**.</span><span class="sxs-lookup"><span data-stu-id="f0763-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="f0763-208">![People](./media/clicktime-tutorial/tic777282.png "People")</span><span class="sxs-lookup"><span data-stu-id="f0763-208">![People](./media/clicktime-tutorial/tic777282.png "People")</span></span>
1. <span data-ttu-id="f0763-209">Click **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="f0763-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="f0763-210">![Add Person](./media/clicktime-tutorial/tic777283.png "Add Person")</span><span class="sxs-lookup"><span data-stu-id="f0763-210">![Add Person](./media/clicktime-tutorial/tic777283.png "Add Person")</span></span>
1. <span data-ttu-id="f0763-211">In the New Person section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0763-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="f0763-212">![People](./media/clicktime-tutorial/tic777284.png "People")</span><span class="sxs-lookup"><span data-stu-id="f0763-212">![People](./media/clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="f0763-213">a.</span><span class="sxs-lookup"><span data-stu-id="f0763-213">a.</span></span>  <span data-ttu-id="f0763-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f0763-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="f0763-215">b.</span><span class="sxs-lookup"><span data-stu-id="f0763-215">b.</span></span>  <span data-ttu-id="f0763-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f0763-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="f0763-217">If you want to, you can set additional properties of the new person object.</span><span class="sxs-lookup"><span data-stu-id="f0763-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="f0763-218">c.</span><span class="sxs-lookup"><span data-stu-id="f0763-218">c.</span></span>  <span data-ttu-id="f0763-219">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f0763-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f0763-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0763-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="f0763-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span><span class="sxs-lookup"><span data-stu-id="f0763-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f0763-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0763-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="f0763-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0763-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f0763-226">In the applications list, select **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="f0763-226">In the applications list, select **ClickTime**.</span></span>

    ![ClickTimne link in the Applications list](./media/clicktime-tutorial/tutorial_clicktime_app.png) 

1. <span data-ttu-id="f0763-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f0763-228">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="f0763-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f0763-230">Click **Add** button.</span></span> <span data-ttu-id="f0763-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0763-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="f0763-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f0763-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f0763-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0763-234">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f0763-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0763-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f0763-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0763-236">Test single sign-on</span></span>

<span data-ttu-id="f0763-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f0763-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0763-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span><span class="sxs-lookup"><span data-stu-id="f0763-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="f0763-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0763-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0763-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f0763-240">Additional resources</span></span>

* [<span data-ttu-id="f0763-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0763-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f0763-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0763-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/clicktime-tutorial/tutorial_general_01.png
[2]: ./media/clicktime-tutorial/tutorial_general_02.png
[3]: ./media/clicktime-tutorial/tutorial_general_03.png
[4]: ./media/clicktime-tutorial/tutorial_general_04.png

[100]: ./media/clicktime-tutorial/tutorial_general_100.png

[200]: ./media/clicktime-tutorial/tutorial_general_200.png
[201]: ./media/clicktime-tutorial/tutorial_general_201.png
[202]: ./media/clicktime-tutorial/tutorial_general_202.png
[203]: ./media/clicktime-tutorial/tutorial_general_203.png

