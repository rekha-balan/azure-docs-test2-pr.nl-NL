---
title: 'Tutorial: Azure Active Directory integration with Vidyard | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Vidyard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bed7df23-6e13-4e7c-b4cc-53ed4804664d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2018
ms.author: jeedes
ms.openlocfilehash: 871942db15d6a3cff45584e33b2191e21d2281a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867642"
---
# <a name="tutorial-azure-active-directory-integration-with-vidyard"></a><span data-ttu-id="b12d8-103">Tutorial: Azure Active Directory integration with Vidyard</span><span class="sxs-lookup"><span data-stu-id="b12d8-103">Tutorial: Azure Active Directory integration with Vidyard</span></span>

<span data-ttu-id="b12d8-104">In this tutorial, you learn how to integrate Vidyard with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b12d8-104">In this tutorial, you learn how to integrate Vidyard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b12d8-105">Integrating Vidyard with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b12d8-105">Integrating Vidyard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b12d8-106">You can control in Azure AD who has access to Vidyard.</span><span class="sxs-lookup"><span data-stu-id="b12d8-106">You can control in Azure AD who has access to Vidyard.</span></span>
- <span data-ttu-id="b12d8-107">You can enable your users to automatically get signed-on to Vidyard (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b12d8-107">You can enable your users to automatically get signed-on to Vidyard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b12d8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b12d8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b12d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b12d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b12d8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b12d8-110">Prerequisites</span></span>

<span data-ttu-id="b12d8-111">To configure Azure AD integration with Vidyard, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b12d8-111">To configure Azure AD integration with Vidyard, you need the following items:</span></span>

- <span data-ttu-id="b12d8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b12d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b12d8-113">A Vidyard single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b12d8-113">A Vidyard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b12d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b12d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b12d8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b12d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b12d8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b12d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b12d8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b12d8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b12d8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b12d8-118">Scenario description</span></span>
<span data-ttu-id="b12d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b12d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b12d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b12d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b12d8-121">Adding Vidyard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b12d8-121">Adding Vidyard from the gallery</span></span>
1. <span data-ttu-id="b12d8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b12d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-vidyard-from-the-gallery"></a><span data-ttu-id="b12d8-123">Adding Vidyard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b12d8-123">Adding Vidyard from the gallery</span></span>
<span data-ttu-id="b12d8-124">To configure the integration of Vidyard into Azure AD, you need to add Vidyard from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b12d8-124">To configure the integration of Vidyard into Azure AD, you need to add Vidyard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b12d8-125">**To add Vidyard from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b12d8-125">**To add Vidyard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b12d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b12d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="b12d8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b12d8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="b12d8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b12d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="b12d8-133">In the search box, type **Vidyard**, select **Vidyard** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b12d8-133">In the search box, type **Vidyard**, select **Vidyard** from result panel then click **Add** button to add the application.</span></span>

    ![Vidyard in the results list](./media/vidyard-tutorial/tutorial_vidyard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b12d8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b12d8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b12d8-136">In this section, you configure and test Azure AD single sign-on with Vidyard based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b12d8-136">In this section, you configure and test Azure AD single sign-on with Vidyard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b12d8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Vidyard is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b12d8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Vidyard is to a user in Azure AD.</span></span> <span data-ttu-id="b12d8-138">In other words, a link relationship between an Azure AD user and the related user in Vidyard needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b12d8-138">In other words, a link relationship between an Azure AD user and the related user in Vidyard needs to be established.</span></span>

<span data-ttu-id="b12d8-139">To configure and test Azure AD single sign-on with Vidyard, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b12d8-139">To configure and test Azure AD single sign-on with Vidyard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b12d8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b12d8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b12d8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b12d8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b12d8-142">**[Create a Vidyard test user](#create-a-vidyard-test-user)** - to have a counterpart of Britta Simon in Vidyard that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b12d8-142">**[Create a Vidyard test user](#create-a-vidyard-test-user)** - to have a counterpart of Britta Simon in Vidyard that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b12d8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b12d8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b12d8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b12d8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b12d8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b12d8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b12d8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Vidyard application.</span><span class="sxs-lookup"><span data-stu-id="b12d8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Vidyard application.</span></span>

<span data-ttu-id="b12d8-147">**To configure Azure AD single sign-on with Vidyard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b12d8-147">**To configure Azure AD single sign-on with Vidyard, perform the following steps:**</span></span>

1. <span data-ttu-id="b12d8-148">In the Azure portal, on the **Vidyard** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-148">In the Azure portal, on the **Vidyard** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="b12d8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b12d8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/vidyard-tutorial/tutorial_vidyard_samlbase.png)

1. <span data-ttu-id="b12d8-152">On the **Vidyard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b12d8-152">On the **Vidyard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Vidyard Domain and URLs single sign-on information](./media/vidyard-tutorial/tutorial_vidyard_url2.png)

    <span data-ttu-id="b12d8-154">a.</span><span class="sxs-lookup"><span data-stu-id="b12d8-154">a.</span></span> <span data-ttu-id="b12d8-155">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="b12d8-155">In the **Identifier** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/metadata`</span></span>

    <span data-ttu-id="b12d8-156">b.</span><span class="sxs-lookup"><span data-stu-id="b12d8-156">b.</span></span> <span data-ttu-id="b12d8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/consume`</span><span class="sxs-lookup"><span data-stu-id="b12d8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/consume`</span></span>

1. <span data-ttu-id="b12d8-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b12d8-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Vidyard Domain and URLs single sign-on information](./media/vidyard-tutorial/tutorial_vidyard_url1.png)

    <span data-ttu-id="b12d8-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/login`</span><span class="sxs-lookup"><span data-stu-id="b12d8-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure.vidyard.com/sso/saml/<unique id>/login`</span></span>

    > [!NOTE]
    > <span data-ttu-id="b12d8-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b12d8-161">These values are not real.</span></span> <span data-ttu-id="b12d8-162">You will update these values with the actual Identifier, Reply URL, and Sign-On URL, which is explained later in the tutorial</span><span class="sxs-lookup"><span data-stu-id="b12d8-162">You will update these values with the actual Identifier, Reply URL, and Sign-On URL, which is explained later in the tutorial</span></span>

1. <span data-ttu-id="b12d8-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b12d8-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/vidyard-tutorial/tutorial_vidyard_certificate.png) 

1. <span data-ttu-id="b12d8-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b12d8-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/vidyard-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b12d8-167">On the **Vidyard Configuration** section, click **Configure Vidyard** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="b12d8-167">On the **Vidyard Configuration** section, click **Configure Vidyard** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b12d8-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="b12d8-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/tutorial_vidyard_configure.png)

1. <span data-ttu-id="b12d8-170">In a different web browser window, log in to your Vidyard Software company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b12d8-170">In a different web browser window, log in to your Vidyard Software company site as an administrator.</span></span>

1. <span data-ttu-id="b12d8-171">From the Vidyard dashboard, select **Group** > **Security**</span><span class="sxs-lookup"><span data-stu-id="b12d8-171">From the Vidyard dashboard, select **Group** > **Security**</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure1.png)

1. <span data-ttu-id="b12d8-173">Click **New Profile** tab.</span><span class="sxs-lookup"><span data-stu-id="b12d8-173">Click **New Profile** tab.</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure2.png)

1. <span data-ttu-id="b12d8-175">In the **SAML Configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b12d8-175">In the **SAML Configuration** section, perform the following steps:</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure3.png)

    <span data-ttu-id="b12d8-177">a.</span><span class="sxs-lookup"><span data-stu-id="b12d8-177">a.</span></span> <span data-ttu-id="b12d8-178">Please enter general profile name in the **Profile Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="b12d8-178">Please enter general profile name in the **Profile Name** textbox.</span></span>

    <span data-ttu-id="b12d8-179">b.</span><span class="sxs-lookup"><span data-stu-id="b12d8-179">b.</span></span> <span data-ttu-id="b12d8-180">Copy **SSO User Login Page** value and paste it into **Sign on URL** textbox in **Vidyard Domain and URLs section** on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b12d8-180">Copy **SSO User Login Page** value and paste it into **Sign on URL** textbox in **Vidyard Domain and URLs section** on Azure portal.</span></span>

    <span data-ttu-id="b12d8-181">c.</span><span class="sxs-lookup"><span data-stu-id="b12d8-181">c.</span></span> <span data-ttu-id="b12d8-182">Copy **ACS URL** value and paste it into **Reply URL** textbox in **Vidyard Domain and URLs section** on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b12d8-182">Copy **ACS URL** value and paste it into **Reply URL** textbox in **Vidyard Domain and URLs section** on Azure portal.</span></span>

    <span data-ttu-id="b12d8-183">d.</span><span class="sxs-lookup"><span data-stu-id="b12d8-183">d.</span></span> <span data-ttu-id="b12d8-184">Copy **Issuer/Metadata URL** value and paste it into **Identifier** textbox in **Vidyard Domain and URLs section** on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b12d8-184">Copy **Issuer/Metadata URL** value and paste it into **Identifier** textbox in **Vidyard Domain and URLs section** on Azure portal.</span></span>

    <span data-ttu-id="b12d8-185">e.</span><span class="sxs-lookup"><span data-stu-id="b12d8-185">e.</span></span> <span data-ttu-id="b12d8-186">Open your downloaded certificate file from Azure portal in Notepad and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="b12d8-186">Open your downloaded certificate file from Azure portal in Notepad and then paste it into the **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="b12d8-187">f.</span><span class="sxs-lookup"><span data-stu-id="b12d8-187">f.</span></span> <span data-ttu-id="b12d8-188">In the **SAML Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b12d8-188">In the **SAML Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    <span data-ttu-id="b12d8-189">g.</span><span class="sxs-lookup"><span data-stu-id="b12d8-189">g.</span></span> <span data-ttu-id="b12d8-190">Click **Confirm**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-190">Click **Confirm**.</span></span>

1. <span data-ttu-id="b12d8-191">From the Single Sign On tab, select **Assign** next to an existing profile</span><span class="sxs-lookup"><span data-stu-id="b12d8-191">From the Single Sign On tab, select **Assign** next to an existing profile</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure4.png)

    > [!NOTE]
    > <span data-ttu-id="b12d8-193">Once you have created an SSO profile, assign it to any group(s) for which users will require access through Azure.</span><span class="sxs-lookup"><span data-stu-id="b12d8-193">Once you have created an SSO profile, assign it to any group(s) for which users will require access through Azure.</span></span> <span data-ttu-id="b12d8-194">If the user does not exist within the group to which they were assigned, Vidyard will automatically create a user account and assign their role in real-time.</span><span class="sxs-lookup"><span data-stu-id="b12d8-194">If the user does not exist within the group to which they were assigned, Vidyard will automatically create a user account and assign their role in real-time.</span></span>

1. <span data-ttu-id="b12d8-195">Select your organization group, which is visible in the **Groups Available to Assign**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-195">Select your organization group, which is visible in the **Groups Available to Assign**.</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure5.png)

1. <span data-ttu-id="b12d8-197">You can see the assigned groups under the **Groups Currently Assigned**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-197">You can see the assigned groups under the **Groups Currently Assigned**.</span></span> <span data-ttu-id="b12d8-198">Select a role for the group as per your organization and click **Confirm**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-198">Select a role for the group as per your organization and click **Confirm**.</span></span>

    ![Vidyard Configuration](./media/vidyard-tutorial/configure6.png)

    > [!NOTE]
    > <span data-ttu-id="b12d8-200">For more information, refer [this doc](https://knowledge.vidyard.com/saml-single-sign-on-authentication/saml-based-single-sign-on-sso-in-vidyard).</span><span class="sxs-lookup"><span data-stu-id="b12d8-200">For more information, refer [this doc](https://knowledge.vidyard.com/saml-single-sign-on-authentication/saml-based-single-sign-on-sso-in-vidyard).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b12d8-201">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b12d8-201">Create an Azure AD test user</span></span>

<span data-ttu-id="b12d8-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b12d8-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b12d8-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b12d8-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b12d8-205">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b12d8-205">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/vidyard-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="b12d8-207">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-207">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/vidyard-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="b12d8-209">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b12d8-209">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/vidyard-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="b12d8-211">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b12d8-211">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/vidyard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b12d8-213">a.</span><span class="sxs-lookup"><span data-stu-id="b12d8-213">a.</span></span> <span data-ttu-id="b12d8-214">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-214">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b12d8-215">b.</span><span class="sxs-lookup"><span data-stu-id="b12d8-215">b.</span></span> <span data-ttu-id="b12d8-216">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b12d8-216">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b12d8-217">c.</span><span class="sxs-lookup"><span data-stu-id="b12d8-217">c.</span></span> <span data-ttu-id="b12d8-218">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b12d8-218">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b12d8-219">d.</span><span class="sxs-lookup"><span data-stu-id="b12d8-219">d.</span></span> <span data-ttu-id="b12d8-220">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-220">Click **Create**.</span></span>
 
### <a name="create-a-vidyard-test-user"></a><span data-ttu-id="b12d8-221">Create a Vidyard test user</span><span class="sxs-lookup"><span data-stu-id="b12d8-221">Create a Vidyard test user</span></span>

<span data-ttu-id="b12d8-222">The objective of this section is to create a user called Britta Simon in Vidyard.</span><span class="sxs-lookup"><span data-stu-id="b12d8-222">The objective of this section is to create a user called Britta Simon in Vidyard.</span></span> <span data-ttu-id="b12d8-223">Vidyard supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b12d8-223">Vidyard supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b12d8-224">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b12d8-224">There is no action item for you in this section.</span></span> <span data-ttu-id="b12d8-225">A new user is created during an attempt to access Vidyard if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="b12d8-225">A new user is created during an attempt to access Vidyard if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="b12d8-226">If you need to create a user manually, contact [Vidyard support team](mailto:support@vidyard.com).</span><span class="sxs-lookup"><span data-stu-id="b12d8-226">If you need to create a user manually, contact [Vidyard support team](mailto:support@vidyard.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b12d8-227">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b12d8-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="b12d8-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Vidyard.</span><span class="sxs-lookup"><span data-stu-id="b12d8-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Vidyard.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b12d8-230">**To assign Britta Simon to Vidyard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b12d8-230">**To assign Britta Simon to Vidyard, perform the following steps:**</span></span>

1. <span data-ttu-id="b12d8-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="b12d8-233">In the applications list, select **Vidyard**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-233">In the applications list, select **Vidyard**.</span></span>

    ![The Vidyard link in the Applications list](./media/vidyard-tutorial/tutorial_vidyard_app.png)  

1. <span data-ttu-id="b12d8-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b12d8-235">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="b12d8-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b12d8-237">Click **Add** button.</span></span> <span data-ttu-id="b12d8-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b12d8-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="b12d8-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b12d8-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b12d8-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b12d8-241">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b12d8-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b12d8-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b12d8-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b12d8-243">Test single sign-on</span></span>

<span data-ttu-id="b12d8-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b12d8-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b12d8-245">When you click the Vidyard tile in the Access Panel, you should get automatically signed-on to your Vidyard application.</span><span class="sxs-lookup"><span data-stu-id="b12d8-245">When you click the Vidyard tile in the Access Panel, you should get automatically signed-on to your Vidyard application.</span></span>
<span data-ttu-id="b12d8-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b12d8-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b12d8-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b12d8-247">Additional resources</span></span>

* [<span data-ttu-id="b12d8-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b12d8-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b12d8-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b12d8-249">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/vidyard-tutorial/tutorial_general_01.png
[2]: ./media/vidyard-tutorial/tutorial_general_02.png
[3]: ./media/vidyard-tutorial/tutorial_general_03.png
[4]: ./media/vidyard-tutorial/tutorial_general_04.png

[100]: ./media/vidyard-tutorial/tutorial_general_100.png

[200]: ./media/vidyard-tutorial/tutorial_general_200.png
[201]: ./media/vidyard-tutorial/tutorial_general_201.png
[202]: ./media/vidyard-tutorial/tutorial_general_202.png
[203]: ./media/vidyard-tutorial/tutorial_general_203.png

