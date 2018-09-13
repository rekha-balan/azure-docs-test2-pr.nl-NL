---
title: 'Tutorial: Azure Active Directory integration with SmartRecruiters | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SmartRecruiters.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: e96aeecd-e113-454e-89c3-58c9f44cfd4c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: jeedes
ms.openlocfilehash: b248cd7d5d45e4f91bc97a5a29476f9bfa03089d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966665"
---
# <a name="tutorial-azure-active-directory-integration-with-smartrecruiters"></a><span data-ttu-id="36c00-103">Tutorial: Azure Active Directory integration with SmartRecruiters</span><span class="sxs-lookup"><span data-stu-id="36c00-103">Tutorial: Azure Active Directory integration with SmartRecruiters</span></span>

<span data-ttu-id="36c00-104">In this tutorial, you learn how to integrate SmartRecruiters with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36c00-104">In this tutorial, you learn how to integrate SmartRecruiters with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36c00-105">Integrating SmartRecruiters with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="36c00-105">Integrating SmartRecruiters with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36c00-106">You can control in Azure AD who has access to SmartRecruiters.</span><span class="sxs-lookup"><span data-stu-id="36c00-106">You can control in Azure AD who has access to SmartRecruiters.</span></span>
- <span data-ttu-id="36c00-107">You can enable your users to automatically get signed-on to SmartRecruiters (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="36c00-107">You can enable your users to automatically get signed-on to SmartRecruiters (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="36c00-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="36c00-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="36c00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="36c00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36c00-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="36c00-110">Prerequisites</span></span>

<span data-ttu-id="36c00-111">To configure Azure AD integration with SmartRecruiters, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="36c00-111">To configure Azure AD integration with SmartRecruiters, you need the following items:</span></span>

- <span data-ttu-id="36c00-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="36c00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36c00-113">A SmartRecruiters single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="36c00-113">A SmartRecruiters single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36c00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="36c00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36c00-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="36c00-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36c00-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="36c00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36c00-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36c00-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36c00-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="36c00-118">Scenario description</span></span>
<span data-ttu-id="36c00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="36c00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36c00-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="36c00-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36c00-121">Adding SmartRecruiters from the gallery</span><span class="sxs-lookup"><span data-stu-id="36c00-121">Adding SmartRecruiters from the gallery</span></span>
1. <span data-ttu-id="36c00-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36c00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smartrecruiters-from-the-gallery"></a><span data-ttu-id="36c00-123">Adding SmartRecruiters from the gallery</span><span class="sxs-lookup"><span data-stu-id="36c00-123">Adding SmartRecruiters from the gallery</span></span>
<span data-ttu-id="36c00-124">To configure the integration of SmartRecruiters into Azure AD, you need to add SmartRecruiters from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="36c00-124">To configure the integration of SmartRecruiters into Azure AD, you need to add SmartRecruiters from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36c00-125">**To add SmartRecruiters from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36c00-125">**To add SmartRecruiters from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36c00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="36c00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="36c00-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="36c00-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36c00-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="36c00-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="36c00-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="36c00-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="36c00-133">In the search box, type **SmartRecruiters**, select **SmartRecruiters** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="36c00-133">In the search box, type **SmartRecruiters**, select **SmartRecruiters** from result panel then click **Add** button to add the application.</span></span>

    ![SmartRecruiters in the results list](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="36c00-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36c00-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="36c00-136">In this section, you configure and test Azure AD single sign-on with SmartRecruiters based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36c00-136">In this section, you configure and test Azure AD single sign-on with SmartRecruiters based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36c00-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SmartRecruiters is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36c00-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SmartRecruiters is to a user in Azure AD.</span></span> <span data-ttu-id="36c00-138">In other words, a link relationship between an Azure AD user and the related user in SmartRecruiters needs to be established.</span><span class="sxs-lookup"><span data-stu-id="36c00-138">In other words, a link relationship between an Azure AD user and the related user in SmartRecruiters needs to be established.</span></span>

<span data-ttu-id="36c00-139">In SmartRecruiters, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="36c00-139">In SmartRecruiters, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36c00-140">To configure and test Azure AD single sign-on with SmartRecruiters, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="36c00-140">To configure and test Azure AD single sign-on with SmartRecruiters, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36c00-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="36c00-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="36c00-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36c00-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="36c00-143">**[Create a SmartRecruiters test user](#create-a-smartrecruiters-test-user)** - to have a counterpart of Britta Simon in SmartRecruiters that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="36c00-143">**[Create a SmartRecruiters test user](#create-a-smartrecruiters-test-user)** - to have a counterpart of Britta Simon in SmartRecruiters that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="36c00-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36c00-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="36c00-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="36c00-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="36c00-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36c00-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="36c00-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmartRecruiters application.</span><span class="sxs-lookup"><span data-stu-id="36c00-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmartRecruiters application.</span></span>

<span data-ttu-id="36c00-148">**To configure Azure AD single sign-on with SmartRecruiters, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36c00-148">**To configure Azure AD single sign-on with SmartRecruiters, perform the following steps:**</span></span>

1. <span data-ttu-id="36c00-149">In the Azure portal, on the **SmartRecruiters** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="36c00-149">In the Azure portal, on the **SmartRecruiters** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="36c00-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36c00-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_samlbase.png)

1. <span data-ttu-id="36c00-153">On the **SmartRecruiters Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="36c00-153">On the **SmartRecruiters Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![SmartRecruiters Domain and URLs single sign-on information](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_url.png)

    <span data-ttu-id="36c00-155">a.</span><span class="sxs-lookup"><span data-stu-id="36c00-155">a.</span></span> <span data-ttu-id="36c00-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="36c00-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>`</span></span>

    <span data-ttu-id="36c00-157">b.</span><span class="sxs-lookup"><span data-stu-id="36c00-157">b.</span></span> <span data-ttu-id="36c00-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>/callback`</span><span class="sxs-lookup"><span data-stu-id="36c00-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>/callback`</span></span>

1. <span data-ttu-id="36c00-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="36c00-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![SmartRecruiters Domain and URLs single sign-on information](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_url1.png)

    <span data-ttu-id="36c00-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>/login`</span><span class="sxs-lookup"><span data-stu-id="36c00-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.smartrecruiters.com/web-sso/saml/<companyname>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="36c00-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="36c00-162">These values are not real.</span></span> <span data-ttu-id="36c00-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="36c00-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="36c00-164">Contact [SmartRecruiters Client support team](https://www.smartrecruiters.com/about-us/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="36c00-164">Contact [SmartRecruiters Client support team](https://www.smartrecruiters.com/about-us/contact-us/) to get these values.</span></span> 

1. <span data-ttu-id="36c00-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate on your computer.</span><span class="sxs-lookup"><span data-stu-id="36c00-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate on your computer.</span></span>

    ![The Certificate download link](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_certificate.png) 

1. <span data-ttu-id="36c00-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="36c00-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/smartrecruiters-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="36c00-169">On the **SmartRecruiters Configuration** section, click **Configure SmartRecruiters** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="36c00-169">On the **SmartRecruiters Configuration** section, click **Configure SmartRecruiters** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36c00-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="36c00-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SmartRecruiters Configuration](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_configure.png) 

1. <span data-ttu-id="36c00-172">In a different web browser window, log in to your SmartRecruiters company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="36c00-172">In a different web browser window, log in to your SmartRecruiters company site as an administrator.</span></span>

1. <span data-ttu-id="36c00-173">Go to **Settings / Admin**.</span><span class="sxs-lookup"><span data-stu-id="36c00-173">Go to **Settings / Admin**.</span></span>

    ![SmartRecruiters Configuration](./media/smartrecruiters-tutorial/configure.png)

1. <span data-ttu-id="36c00-175">In the **Configuration** section, click **Web SSO**.</span><span class="sxs-lookup"><span data-stu-id="36c00-175">In the **Configuration** section, click **Web SSO**.</span></span>

    ![SmartRecruiters Configuration](./media/smartrecruiters-tutorial/configure1.png)

1. <span data-ttu-id="36c00-177">Toggle **Enable Web SSO**.</span><span class="sxs-lookup"><span data-stu-id="36c00-177">Toggle **Enable Web SSO**.</span></span>

    ![SmartRecruiters Configuration](./media/smartrecruiters-tutorial/configure2.png)

1. <span data-ttu-id="36c00-179">In **Identity Provider Configuration**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36c00-179">In **Identity Provider Configuration**, perform the following steps:</span></span>

    ![SmartRecruiters Configuration](./media/smartrecruiters-tutorial/configure4.png)

    <span data-ttu-id="36c00-181">a.</span><span class="sxs-lookup"><span data-stu-id="36c00-181">a.</span></span> <span data-ttu-id="36c00-182">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="36c00-182">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="36c00-183">b.</span><span class="sxs-lookup"><span data-stu-id="36c00-183">b.</span></span> <span data-ttu-id="36c00-184">Open **certificate(Base64)** which you have downloaded from Azure portal and paste the value into **Identity Provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="36c00-184">Open **certificate(Base64)** which you have downloaded from Azure portal and paste the value into **Identity Provider certificate** textbox.</span></span>

1. <span data-ttu-id="36c00-185">Click **Save Web SSO configuration**.</span><span class="sxs-lookup"><span data-stu-id="36c00-185">Click **Save Web SSO configuration**.</span></span>

> [!TIP]
> <span data-ttu-id="36c00-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="36c00-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36c00-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="36c00-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36c00-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36c00-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="36c00-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36c00-189">Create an Azure AD test user</span></span>

<span data-ttu-id="36c00-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36c00-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="36c00-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36c00-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36c00-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="36c00-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/smartrecruiters-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="36c00-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="36c00-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/smartrecruiters-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="36c00-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="36c00-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/smartrecruiters-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="36c00-199">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36c00-199">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/smartrecruiters-tutorial/create_aaduser_04.png)

    <span data-ttu-id="36c00-201">a.</span><span class="sxs-lookup"><span data-stu-id="36c00-201">a.</span></span> <span data-ttu-id="36c00-202">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36c00-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36c00-203">b.</span><span class="sxs-lookup"><span data-stu-id="36c00-203">b.</span></span> <span data-ttu-id="36c00-204">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36c00-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="36c00-205">c.</span><span class="sxs-lookup"><span data-stu-id="36c00-205">c.</span></span> <span data-ttu-id="36c00-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="36c00-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="36c00-207">d.</span><span class="sxs-lookup"><span data-stu-id="36c00-207">d.</span></span> <span data-ttu-id="36c00-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="36c00-208">Click **Create**.</span></span>
 
### <a name="create-a-smartrecruiters-test-user"></a><span data-ttu-id="36c00-209">Create a SmartRecruiters test user</span><span class="sxs-lookup"><span data-stu-id="36c00-209">Create a SmartRecruiters test user</span></span>

<span data-ttu-id="36c00-210">In this section, you create a user called Britta Simon in SmartRecruiters.</span><span class="sxs-lookup"><span data-stu-id="36c00-210">In this section, you create a user called Britta Simon in SmartRecruiters.</span></span> <span data-ttu-id="36c00-211">Work with [SmartRecruiters support team](https://www.smartrecruiters.com/about-us/contact-us/) to add the users in the SmartRecruiters platform.</span><span class="sxs-lookup"><span data-stu-id="36c00-211">Work with [SmartRecruiters support team](https://www.smartrecruiters.com/about-us/contact-us/) to add the users in the SmartRecruiters platform.</span></span> <span data-ttu-id="36c00-212">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36c00-212">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="36c00-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36c00-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="36c00-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmartRecruiters.</span><span class="sxs-lookup"><span data-stu-id="36c00-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmartRecruiters.</span></span>

![Assign the user role][200] 

<span data-ttu-id="36c00-216">**To assign Britta Simon to SmartRecruiters, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36c00-216">**To assign Britta Simon to SmartRecruiters, perform the following steps:**</span></span>

1. <span data-ttu-id="36c00-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="36c00-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="36c00-219">In the applications list, select **SmartRecruiters**.</span><span class="sxs-lookup"><span data-stu-id="36c00-219">In the applications list, select **SmartRecruiters**.</span></span>

    ![The SmartRecruiters link in the Applications list](./media/smartrecruiters-tutorial/tutorial_smartrecruiters_app.png)  

1. <span data-ttu-id="36c00-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="36c00-221">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="36c00-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="36c00-223">Click **Add** button.</span></span> <span data-ttu-id="36c00-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="36c00-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="36c00-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="36c00-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="36c00-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="36c00-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="36c00-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="36c00-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="36c00-229">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="36c00-229">Test single sign-on</span></span>

<span data-ttu-id="36c00-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="36c00-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36c00-231">When you click the SmartRecruiters tile in the Access Panel, you should get automatically signed-on to your SmartRecruiters application.</span><span class="sxs-lookup"><span data-stu-id="36c00-231">When you click the SmartRecruiters tile in the Access Panel, you should get automatically signed-on to your SmartRecruiters application.</span></span>
<span data-ttu-id="36c00-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36c00-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="36c00-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="36c00-233">Additional resources</span></span>

* [<span data-ttu-id="36c00-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36c00-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="36c00-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36c00-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/smartrecruiters-tutorial/tutorial_general_01.png
[2]: ./media/smartrecruiters-tutorial/tutorial_general_02.png
[3]: ./media/smartrecruiters-tutorial/tutorial_general_03.png
[4]: ./media/smartrecruiters-tutorial/tutorial_general_04.png

[100]: ./media/smartrecruiters-tutorial/tutorial_general_100.png

[200]: ./media/smartrecruiters-tutorial/tutorial_general_200.png
[201]: ./media/smartrecruiters-tutorial/tutorial_general_201.png
[202]: ./media/smartrecruiters-tutorial/tutorial_general_202.png
[203]: ./media/smartrecruiters-tutorial/tutorial_general_203.png

