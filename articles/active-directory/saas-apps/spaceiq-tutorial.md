---
title: 'Tutorial: Azure Active Directory integration with SpaceIQ | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SpaceIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 5b55ae29-491f-401f-9299-d3a6b64a1b99
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2017
ms.author: jeedes
ms.openlocfilehash: 515b89502a9794671c1086b9dc537cdac9779f79
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967840"
---
# <a name="tutorial-azure-active-directory-integration-with-spaceiq"></a><span data-ttu-id="c5959-103">Tutorial: Azure Active Directory integration with SpaceIQ</span><span class="sxs-lookup"><span data-stu-id="c5959-103">Tutorial: Azure Active Directory integration with SpaceIQ</span></span>

<span data-ttu-id="c5959-104">In this tutorial, you learn how to integrate SpaceIQ with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5959-104">In this tutorial, you learn how to integrate SpaceIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5959-105">Integrating SpaceIQ with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c5959-105">Integrating SpaceIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5959-106">You can control in Azure AD who has access to SpaceIQ.</span><span class="sxs-lookup"><span data-stu-id="c5959-106">You can control in Azure AD who has access to SpaceIQ.</span></span>
- <span data-ttu-id="c5959-107">You can enable your users to automatically get signed-on to SpaceIQ (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c5959-107">You can enable your users to automatically get signed-on to SpaceIQ (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c5959-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c5959-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c5959-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c5959-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5959-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5959-110">Prerequisites</span></span>

<span data-ttu-id="c5959-111">To configure Azure AD integration with SpaceIQ, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c5959-111">To configure Azure AD integration with SpaceIQ, you need the following items:</span></span>

- <span data-ttu-id="c5959-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c5959-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5959-113">A SpaceIQ single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c5959-113">A SpaceIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5959-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c5959-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5959-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c5959-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5959-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c5959-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5959-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5959-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5959-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c5959-118">Scenario description</span></span>
<span data-ttu-id="c5959-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c5959-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5959-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c5959-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5959-121">Adding SpaceIQ from the gallery</span><span class="sxs-lookup"><span data-stu-id="c5959-121">Adding SpaceIQ from the gallery</span></span>
1. <span data-ttu-id="c5959-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5959-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-spaceiq-from-the-gallery"></a><span data-ttu-id="c5959-123">Adding SpaceIQ from the gallery</span><span class="sxs-lookup"><span data-stu-id="c5959-123">Adding SpaceIQ from the gallery</span></span>
<span data-ttu-id="c5959-124">To configure the integration of SpaceIQ into Azure AD, you need to add SpaceIQ from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c5959-124">To configure the integration of SpaceIQ into Azure AD, you need to add SpaceIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5959-125">**To add SpaceIQ from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5959-125">**To add SpaceIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5959-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c5959-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c5959-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c5959-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5959-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c5959-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c5959-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c5959-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c5959-133">In the search box, type **SpaceIQ**, select **SpaceIQ** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c5959-133">In the search box, type **SpaceIQ**, select **SpaceIQ** from result panel then click **Add** button to add the application.</span></span>

    ![SpaceIQ in the results list](./media/spaceiq-tutorial/tutorial_spaceiq_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c5959-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5959-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c5959-136">In this section, you configure and test Azure AD single sign-on with SpaceIQ based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c5959-136">In this section, you configure and test Azure AD single sign-on with SpaceIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c5959-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SpaceIQ is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5959-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SpaceIQ is to a user in Azure AD.</span></span> <span data-ttu-id="c5959-138">In other words, a link relationship between an Azure AD user and the related user in SpaceIQ needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c5959-138">In other words, a link relationship between an Azure AD user and the related user in SpaceIQ needs to be established.</span></span>

<span data-ttu-id="c5959-139">In SpaceIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c5959-139">In SpaceIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5959-140">To configure and test Azure AD single sign-on with SpaceIQ, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c5959-140">To configure and test Azure AD single sign-on with SpaceIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5959-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c5959-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c5959-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5959-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c5959-143">**[Create a SpaceIQ test user](#create-a-spaceiq-test-user)** - to have a counterpart of Britta Simon in SpaceIQ that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c5959-143">**[Create a SpaceIQ test user](#create-a-spaceiq-test-user)** - to have a counterpart of Britta Simon in SpaceIQ that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c5959-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5959-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c5959-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c5959-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c5959-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5959-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c5959-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpaceIQ application.</span><span class="sxs-lookup"><span data-stu-id="c5959-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpaceIQ application.</span></span>

<span data-ttu-id="c5959-148">**To configure Azure AD single sign-on with SpaceIQ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5959-148">**To configure Azure AD single sign-on with SpaceIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="c5959-149">In the Azure portal, on the **SpaceIQ** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c5959-149">In the Azure portal, on the **SpaceIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c5959-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5959-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/spaceiq-tutorial/tutorial_spaceiq_samlbase.png)

1. <span data-ttu-id="c5959-153">On the **SpaceIQ Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c5959-153">On the **SpaceIQ Domain and URLs** section, perform the following steps:</span></span>

    ![SpaceIQ Domain and URLs single sign-on information](./media/spaceiq-tutorial/tutorial_spaceiq_url.png)

    <span data-ttu-id="c5959-155">a.</span><span class="sxs-lookup"><span data-stu-id="c5959-155">a.</span></span> <span data-ttu-id="c5959-156">In the **Identifier** textbox, type the URL: `https://api.spaceiq.com`</span><span class="sxs-lookup"><span data-stu-id="c5959-156">In the **Identifier** textbox, type the URL: `https://api.spaceiq.com`</span></span>

    <span data-ttu-id="c5959-157">b.</span><span class="sxs-lookup"><span data-stu-id="c5959-157">b.</span></span> <span data-ttu-id="c5959-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.spaceiq.com/saml/<instanceid>/callback`</span><span class="sxs-lookup"><span data-stu-id="c5959-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.spaceiq.com/saml/<instanceid>/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5959-159">Update these values with the actual Reply URL and identifier which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c5959-159">Update these values with the actual Reply URL and identifier which is explained later in the tutorial.</span></span>
 
1. <span data-ttu-id="c5959-160">On the **SAML Signing Certificate** section, click **(Certificate Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c5959-160">On the **SAML Signing Certificate** section, click **(Certificate Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/spaceiq-tutorial/tutorial_spaceiq_certificate.png) 

1. <span data-ttu-id="c5959-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c5959-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/spaceiq-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c5959-164">On the **SpaceIQ Configuration** section, click **Configure SpaceIQ** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c5959-164">On the **SpaceIQ Configuration** section, click **Configure SpaceIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c5959-165">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c5959-165">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![SpaceIQ Configuration](./media/spaceiq-tutorial/tutorial_spaceiq_configure.png) 

1.  <span data-ttu-id="c5959-167">Open a new browser window, and then sign in to your SpaceIQ environment as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c5959-167">Open a new browser window, and then sign in to your SpaceIQ environment as an administrator.</span></span>

1. <span data-ttu-id="c5959-168">Once you are logged in, click on the puzzle sign at the top right, then click on **"Integrations"**</span><span class="sxs-lookup"><span data-stu-id="c5959-168">Once you are logged in, click on the puzzle sign at the top right, then click on **"Integrations"**</span></span>

    ![Account settings](./media/spaceiq-tutorial/setting1.png) 

1. <span data-ttu-id="c5959-170">Under **All PROVISIONING & SSO**, click on the **Azure** tile to add an instance of Azure as IDP.</span><span class="sxs-lookup"><span data-stu-id="c5959-170">Under **All PROVISIONING & SSO**, click on the **Azure** tile to add an instance of Azure as IDP.</span></span>

    ![SAML icon](./media/spaceiq-tutorial/setting2.png)

1. <span data-ttu-id="c5959-172">In the **SSO** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c5959-172">In the **SSO** dialog box, perform the following steps:</span></span>

    ![SAML Authentication Settings](./media/spaceiq-tutorial/setting3.png)

    <span data-ttu-id="c5959-174">a.</span><span class="sxs-lookup"><span data-stu-id="c5959-174">a.</span></span> <span data-ttu-id="c5959-175">In the **SAML Issuer URL** box, paste the **SAML Entity ID** value copied from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="c5959-175">In the **SAML Issuer URL** box, paste the **SAML Entity ID** value copied from the Azure AD application configuration window.</span></span>
    
    <span data-ttu-id="c5959-176">b.</span><span class="sxs-lookup"><span data-stu-id="c5959-176">b.</span></span> <span data-ttu-id="c5959-177">Copy the **SAML CallBack Endpoint URL (read-only)** value and paste the value in the **Reply URL** box in the Azure portal, under SpaceIQ **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="c5959-177">Copy the **SAML CallBack Endpoint URL (read-only)** value and paste the value in the **Reply URL** box in the Azure portal, under SpaceIQ **Domain and URLs** section.</span></span>
    
    <span data-ttu-id="c5959-178">c.</span><span class="sxs-lookup"><span data-stu-id="c5959-178">c.</span></span> <span data-ttu-id="c5959-179">Copy the **SAML Audience URI (read-only)** value and paste the value in the **Identifier** box in the Azure portal, under SpaceIQ **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="c5959-179">Copy the **SAML Audience URI (read-only)** value and paste the value in the **Identifier** box in the Azure portal, under SpaceIQ **Domain and URLs** section.</span></span>

    <span data-ttu-id="c5959-180">d.</span><span class="sxs-lookup"><span data-stu-id="c5959-180">d.</span></span> <span data-ttu-id="c5959-181">Open the downloaded certificate file in notepad, copy the content, and then paste it in the **X.509 Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="c5959-181">Open the downloaded certificate file in notepad, copy the content, and then paste it in the **X.509 Certificate** box.</span></span>
    
    <span data-ttu-id="c5959-182">e.</span><span class="sxs-lookup"><span data-stu-id="c5959-182">e.</span></span> <span data-ttu-id="c5959-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c5959-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c5959-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c5959-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5959-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c5959-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5959-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5959-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c5959-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c5959-187">Create an Azure AD test user</span></span>

<span data-ttu-id="c5959-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5959-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c5959-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5959-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5959-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c5959-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/spaceiq-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c5959-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c5959-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/spaceiq-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c5959-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c5959-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/spaceiq-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c5959-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c5959-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/spaceiq-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c5959-199">a.</span><span class="sxs-lookup"><span data-stu-id="c5959-199">a.</span></span> <span data-ttu-id="c5959-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5959-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5959-201">b.</span><span class="sxs-lookup"><span data-stu-id="c5959-201">b.</span></span> <span data-ttu-id="c5959-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5959-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c5959-203">c.</span><span class="sxs-lookup"><span data-stu-id="c5959-203">c.</span></span> <span data-ttu-id="c5959-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c5959-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c5959-205">d.</span><span class="sxs-lookup"><span data-stu-id="c5959-205">d.</span></span> <span data-ttu-id="c5959-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5959-206">Click **Create**.</span></span>
  
### <a name="create-a-spaceiq-test-user"></a><span data-ttu-id="c5959-207">Create a SpaceIQ test user</span><span class="sxs-lookup"><span data-stu-id="c5959-207">Create a SpaceIQ test user</span></span>

<span data-ttu-id="c5959-208">In this section, you create a user called Britta Simon in SpaceIQ.</span><span class="sxs-lookup"><span data-stu-id="c5959-208">In this section, you create a user called Britta Simon in SpaceIQ.</span></span> <span data-ttu-id="c5959-209">Work [SpaceIQ support team](mailto:eng@spaceiq.com) to add the users in the SpaceIQ platform.</span><span class="sxs-lookup"><span data-stu-id="c5959-209">Work [SpaceIQ support team](mailto:eng@spaceiq.com) to add the users in the SpaceIQ platform.</span></span> <span data-ttu-id="c5959-210">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5959-210">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c5959-211">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c5959-211">Assign the Azure AD test user</span></span>

<span data-ttu-id="c5959-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpaceIQ.</span><span class="sxs-lookup"><span data-stu-id="c5959-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpaceIQ.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c5959-214">**To assign Britta Simon to SpaceIQ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5959-214">**To assign Britta Simon to SpaceIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="c5959-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c5959-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c5959-217">In the applications list, select **SpaceIQ**.</span><span class="sxs-lookup"><span data-stu-id="c5959-217">In the applications list, select **SpaceIQ**.</span></span>

    ![The SpaceIQ link in the Applications list](./media/spaceiq-tutorial/tutorial_spaceiq_app.png)  

1. <span data-ttu-id="c5959-219">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c5959-219">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c5959-221">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c5959-221">Click **Add** button.</span></span> <span data-ttu-id="c5959-222">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5959-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c5959-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c5959-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c5959-225">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5959-225">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c5959-226">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5959-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c5959-227">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5959-227">Test single sign-on</span></span>

<span data-ttu-id="c5959-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c5959-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c5959-229">When you click the SpaceIQ tile in the Access Panel, you should get automatically signed-on to your SpaceIQ application.</span><span class="sxs-lookup"><span data-stu-id="c5959-229">When you click the SpaceIQ tile in the Access Panel, you should get automatically signed-on to your SpaceIQ application.</span></span>
<span data-ttu-id="c5959-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5959-230">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5959-231">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c5959-231">Additional resources</span></span>

* [<span data-ttu-id="c5959-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5959-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c5959-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5959-233">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/spaceiq-tutorial/tutorial_general_01.png
[2]: ./media/spaceiq-tutorial/tutorial_general_02.png
[3]: ./media/spaceiq-tutorial/tutorial_general_03.png
[4]: ./media/spaceiq-tutorial/tutorial_general_04.png

[100]: ./media/spaceiq-tutorial/tutorial_general_100.png

[200]: ./media/spaceiq-tutorial/tutorial_general_200.png
[201]: ./media/spaceiq-tutorial/tutorial_general_201.png
[202]: ./media/spaceiq-tutorial/tutorial_general_202.png
[203]: ./media/spaceiq-tutorial/tutorial_general_203.png

