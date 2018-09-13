---
title: 'Tutorial: Azure Active Directory integration with Voyance | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: ce72fb75729574c9645025459b67fd3eab597bb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870476"
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="60ce2-103">Tutorial: Azure Active Directory integration with Voyance</span><span class="sxs-lookup"><span data-stu-id="60ce2-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="60ce2-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60ce2-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60ce2-105">Integrating Voyance with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="60ce2-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60ce2-106">You can control in Azure AD who has access to Voyance</span><span class="sxs-lookup"><span data-stu-id="60ce2-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="60ce2-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="60ce2-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60ce2-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="60ce2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60ce2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="60ce2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60ce2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="60ce2-110">Prerequisites</span></span>

<span data-ttu-id="60ce2-111">To configure Azure AD integration with Voyance, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="60ce2-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="60ce2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="60ce2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60ce2-113">A Voyance single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="60ce2-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60ce2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="60ce2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60ce2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="60ce2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60ce2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="60ce2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60ce2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60ce2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60ce2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="60ce2-118">Scenario description</span></span>
<span data-ttu-id="60ce2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="60ce2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60ce2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="60ce2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60ce2-121">Adding Voyance from the gallery</span><span class="sxs-lookup"><span data-stu-id="60ce2-121">Adding Voyance from the gallery</span></span>
1. <span data-ttu-id="60ce2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60ce2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="60ce2-123">Adding Voyance from the gallery</span><span class="sxs-lookup"><span data-stu-id="60ce2-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="60ce2-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="60ce2-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60ce2-125">**To add Voyance from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60ce2-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60ce2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="60ce2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="60ce2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60ce2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="60ce2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="60ce2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="60ce2-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="60ce2-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance  in the results list](./media/voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="60ce2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60ce2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="60ce2-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60ce2-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60ce2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60ce2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="60ce2-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span><span class="sxs-lookup"><span data-stu-id="60ce2-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="60ce2-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="60ce2-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60ce2-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="60ce2-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60ce2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="60ce2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="60ce2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60ce2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="60ce2-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="60ce2-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="60ce2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60ce2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="60ce2-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="60ce2-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="60ce2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60ce2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="60ce2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span><span class="sxs-lookup"><span data-stu-id="60ce2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="60ce2-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60ce2-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="60ce2-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="60ce2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60ce2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/voyance-tutorial/tutorial_voyance_samlbase.png)

1. <span data-ttu-id="60ce2-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="60ce2-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Voyance Domain and URLs single sign-on information for IDP](./media/voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="60ce2-155">a.</span><span class="sxs-lookup"><span data-stu-id="60ce2-155">a.</span></span> <span data-ttu-id="60ce2-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="60ce2-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="60ce2-157">b.</span><span class="sxs-lookup"><span data-stu-id="60ce2-157">b.</span></span> <span data-ttu-id="60ce2-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="60ce2-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

1. <span data-ttu-id="60ce2-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="60ce2-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Voyance Domain and URLs single sign-on information for SP](./media/voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="60ce2-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="60ce2-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="60ce2-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="60ce2-162">These values are not real.</span></span> <span data-ttu-id="60ce2-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="60ce2-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="60ce2-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="60ce2-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

1. <span data-ttu-id="60ce2-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="60ce2-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/voyance-tutorial/tutorial_voyance_certificate.png) 

1. <span data-ttu-id="60ce2-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="60ce2-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/voyance-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="60ce2-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="60ce2-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60ce2-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="60ce2-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Voyance configuration](./media/voyance-tutorial/tutorial_voyance_configure.png) 

1. <span data-ttu-id="60ce2-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="60ce2-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

1. <span data-ttu-id="60ce2-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="60ce2-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Configure Single Sign-On On App Side Acme University](./media/voyance-tutorial/tutorial_voyance_001.png) 

1. <span data-ttu-id="60ce2-175">Click "**Admin Settings**".</span><span class="sxs-lookup"><span data-stu-id="60ce2-175">Click "**Admin Settings**".</span></span>

    ![Configure Single Sign-On On App Side Admin Settings](./media/voyance-tutorial/tutorial_voyance_002.png)

1. <span data-ttu-id="60ce2-177">Click "**User Access**" tab.</span><span class="sxs-lookup"><span data-stu-id="60ce2-177">Click "**User Access**" tab.</span></span>

    ![Configure Single Sign-On On App Side User Access](./media/voyance-tutorial/tutorial_voyance_003.png)

1. <span data-ttu-id="60ce2-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="60ce2-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configure Single Sign-On On App Side SSO is disabled button](./media/voyance-tutorial/tutorial_voyance_004.png)

1. <span data-ttu-id="60ce2-181">Go to **SAML v2** section and perform below steps:</span><span class="sxs-lookup"><span data-stu-id="60ce2-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configure Single Sign-On On App Side SAML v2](./media/voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="60ce2-183">a.</span><span class="sxs-lookup"><span data-stu-id="60ce2-183">a.</span></span> <span data-ttu-id="60ce2-184">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="60ce2-185">b.</span><span class="sxs-lookup"><span data-stu-id="60ce2-185">b.</span></span> <span data-ttu-id="60ce2-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="60ce2-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="60ce2-187">c.</span><span class="sxs-lookup"><span data-stu-id="60ce2-187">c.</span></span> <span data-ttu-id="60ce2-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span><span class="sxs-lookup"><span data-stu-id="60ce2-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="60ce2-189">d.</span><span class="sxs-lookup"><span data-stu-id="60ce2-189">d.</span></span> <span data-ttu-id="60ce2-190">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="60ce2-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="60ce2-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60ce2-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="60ce2-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60ce2-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60ce2-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="60ce2-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60ce2-194">Create an Azure AD test user</span></span>

<span data-ttu-id="60ce2-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60ce2-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="60ce2-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60ce2-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60ce2-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="60ce2-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/voyance-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="60ce2-200">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/voyance-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="60ce2-202">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="60ce2-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/voyance-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="60ce2-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60ce2-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60ce2-206">a.</span><span class="sxs-lookup"><span data-stu-id="60ce2-206">a.</span></span> <span data-ttu-id="60ce2-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60ce2-208">b.</span><span class="sxs-lookup"><span data-stu-id="60ce2-208">b.</span></span> <span data-ttu-id="60ce2-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60ce2-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60ce2-210">c.</span><span class="sxs-lookup"><span data-stu-id="60ce2-210">c.</span></span> <span data-ttu-id="60ce2-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60ce2-212">d.</span><span class="sxs-lookup"><span data-stu-id="60ce2-212">d.</span></span> <span data-ttu-id="60ce2-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="60ce2-214">Create a Voyance test user</span><span class="sxs-lookup"><span data-stu-id="60ce2-214">Create a Voyance test user</span></span>

<span data-ttu-id="60ce2-215">The objective of this section is to create a user called Britta Simon in Voyance.</span><span class="sxs-lookup"><span data-stu-id="60ce2-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="60ce2-216">Voyance supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="60ce2-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="60ce2-217">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="60ce2-217">There is no action item for you in this section.</span></span> <span data-ttu-id="60ce2-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="60ce2-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="60ce2-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="60ce2-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="60ce2-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60ce2-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="60ce2-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span><span class="sxs-lookup"><span data-stu-id="60ce2-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Assign the user role][200]

<span data-ttu-id="60ce2-223">**To assign Britta Simon to Voyance, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60ce2-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="60ce2-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="60ce2-226">In the applications list, select **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-226">In the applications list, select **Voyance**.</span></span>

    ![The Voyance link in the Applications list](./media/voyance-tutorial/tutorial_voyance_app.png) 

1. <span data-ttu-id="60ce2-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="60ce2-228">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="60ce2-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="60ce2-230">Click **Add** button.</span></span> <span data-ttu-id="60ce2-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60ce2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="60ce2-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="60ce2-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="60ce2-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="60ce2-234">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="60ce2-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60ce2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="60ce2-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="60ce2-236">Test single sign-on</span></span>

<span data-ttu-id="60ce2-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="60ce2-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60ce2-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span><span class="sxs-lookup"><span data-stu-id="60ce2-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60ce2-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="60ce2-239">Additional resources</span></span>

* [<span data-ttu-id="60ce2-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60ce2-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="60ce2-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60ce2-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/voyance-tutorial/tutorial_general_01.png
[2]: ./media/voyance-tutorial/tutorial_general_02.png
[3]: ./media/voyance-tutorial/tutorial_general_03.png
[4]: ./media/voyance-tutorial/tutorial_general_04.png

[100]: ./media/voyance-tutorial/tutorial_general_100.png

[200]: ./media/voyance-tutorial/tutorial_general_200.png
[201]: ./media/voyance-tutorial/tutorial_general_201.png
[202]: ./media/voyance-tutorial/tutorial_general_202.png
[203]: ./media/voyance-tutorial/tutorial_general_203.png

