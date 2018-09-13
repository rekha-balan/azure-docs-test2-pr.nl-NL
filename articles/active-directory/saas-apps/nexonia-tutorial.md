---
title: 'Tutorial: Azure Active Directory integration with Nexonia | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Nexonia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2018
ms.author: jeedes
ms.openlocfilehash: 9349164c4386fb32c717b60f132b902d987fc3a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869039"
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="c3be2-103">Tutorial: Azure Active Directory integration with Nexonia</span><span class="sxs-lookup"><span data-stu-id="c3be2-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="c3be2-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3be2-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3be2-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c3be2-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3be2-106">You can control in Azure AD who has access to Nexonia.</span><span class="sxs-lookup"><span data-stu-id="c3be2-106">You can control in Azure AD who has access to Nexonia.</span></span>
- <span data-ttu-id="c3be2-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c3be2-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c3be2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c3be2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c3be2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c3be2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3be2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3be2-110">Prerequisites</span></span>

<span data-ttu-id="c3be2-111">To configure Azure AD integration with Nexonia, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c3be2-111">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="c3be2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c3be2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3be2-113">A Nexonia single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c3be2-113">A Nexonia single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3be2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c3be2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3be2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c3be2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3be2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c3be2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3be2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3be2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3be2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c3be2-118">Scenario description</span></span>
<span data-ttu-id="c3be2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c3be2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3be2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3be2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3be2-121">Adding Nexonia from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3be2-121">Adding Nexonia from the gallery</span></span>
1. <span data-ttu-id="c3be2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3be2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="c3be2-123">Adding Nexonia from the gallery</span><span class="sxs-lookup"><span data-stu-id="c3be2-123">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="c3be2-124">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c3be2-124">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3be2-125">**To add Nexonia from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3be2-125">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3be2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c3be2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c3be2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3be2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c3be2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c3be2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c3be2-133">In the search box, type **Nexonia**, select **Nexonia** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c3be2-133">In the search box, type **Nexonia**, select **Nexonia** from result panel then click **Add** button to add the application.</span></span>

    ![Nexonia in the results list](./media/nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c3be2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3be2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c3be2-136">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c3be2-136">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3be2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3be2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="c3be2-138">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c3be2-138">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="c3be2-139">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c3be2-139">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3be2-140">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c3be2-140">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3be2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c3be2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c3be2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3be2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c3be2-143">**[Create a Nexonia test user](#create-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c3be2-143">**[Create a Nexonia test user](#create-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c3be2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3be2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c3be2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c3be2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c3be2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3be2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c3be2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span><span class="sxs-lookup"><span data-stu-id="c3be2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

  > [!Note]
   > <span data-ttu-id="c3be2-148">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery) for troubleshooting guide.</span><span class="sxs-lookup"><span data-stu-id="c3be2-148">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery) for troubleshooting guide.</span></span> <span data-ttu-id="c3be2-149">If you still have not found the solution, then raise the support request from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c3be2-149">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="c3be2-150">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3be2-150">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="c3be2-151">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-151">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c3be2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3be2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/nexonia-tutorial/tutorial_nexonia_samlbase.png)

1. <span data-ttu-id="c3be2-155">On the **Nexonia Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3be2-155">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Nexonia Domain and URLs single sign-on information](./media/nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="c3be2-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3be2-157">a.</span></span> <span data-ttu-id="c3be2-158">In the **Identifier** textbox, type a value: `Nexonia`</span><span class="sxs-lookup"><span data-stu-id="c3be2-158">In the **Identifier** textbox, type a value: `Nexonia`</span></span>

    <span data-ttu-id="c3be2-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3be2-159">b.</span></span> <span data-ttu-id="c3be2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="c3be2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3be2-161">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="c3be2-161">The Reply URL value is not real.</span></span> <span data-ttu-id="c3be2-162">Update the value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="c3be2-162">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="c3be2-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get the value.</span><span class="sxs-lookup"><span data-stu-id="c3be2-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get the value.</span></span>
 
1. <span data-ttu-id="c3be2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c3be2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/nexonia-tutorial/tutorial_nexonia_certificate.png) 

1. <span data-ttu-id="c3be2-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c3be2-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/nexonia-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c3be2-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c3be2-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c3be2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c3be2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Nexonia Configuration](./media/nexonia-tutorial/tutorial_nexonia_configure.png) 

1. <span data-ttu-id="c3be2-171">To configure single sign-on on **Nexonia** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** and **SAML Entity ID** to [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="c3be2-171">To configure single sign-on on **Nexonia** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** and **SAML Entity ID** to [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new).</span></span> <span data-ttu-id="c3be2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="c3be2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c3be2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c3be2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3be2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c3be2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3be2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3be2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c3be2-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3be2-176">Create an Azure AD test user</span></span>

<span data-ttu-id="c3be2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3be2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c3be2-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3be2-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3be2-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c3be2-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/nexonia-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c3be2-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/nexonia-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c3be2-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c3be2-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/nexonia-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c3be2-186">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c3be2-186">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/nexonia-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c3be2-188">a.</span><span class="sxs-lookup"><span data-stu-id="c3be2-188">a.</span></span> <span data-ttu-id="c3be2-189">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3be2-190">b.</span><span class="sxs-lookup"><span data-stu-id="c3be2-190">b.</span></span> <span data-ttu-id="c3be2-191">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3be2-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c3be2-192">c.</span><span class="sxs-lookup"><span data-stu-id="c3be2-192">c.</span></span> <span data-ttu-id="c3be2-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c3be2-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c3be2-194">d.</span><span class="sxs-lookup"><span data-stu-id="c3be2-194">d.</span></span> <span data-ttu-id="c3be2-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-195">Click **Create**.</span></span>
  
### <a name="create-a-nexonia-test-user"></a><span data-ttu-id="c3be2-196">Create a Nexonia test user</span><span class="sxs-lookup"><span data-stu-id="c3be2-196">Create a Nexonia test user</span></span>

<span data-ttu-id="c3be2-197">In this section, you create a user called Britta Simon in Nexonia.</span><span class="sxs-lookup"><span data-stu-id="c3be2-197">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="c3be2-198">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span><span class="sxs-lookup"><span data-stu-id="c3be2-198">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="c3be2-199">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3be2-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c3be2-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c3be2-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="c3be2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span><span class="sxs-lookup"><span data-stu-id="c3be2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c3be2-203">**To assign Britta Simon to Nexonia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c3be2-203">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="c3be2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c3be2-206">In the applications list, select **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-206">In the applications list, select **Nexonia**.</span></span>

    ![The Nexonia link in the Applications list](./media/nexonia-tutorial/tutorial_nexonia_app.png)  

1. <span data-ttu-id="c3be2-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c3be2-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c3be2-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c3be2-210">Click **Add** button.</span></span> <span data-ttu-id="c3be2-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c3be2-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c3be2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c3be2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c3be2-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c3be2-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c3be2-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c3be2-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c3be2-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c3be2-216">Test single sign-on</span></span>

<span data-ttu-id="c3be2-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3be2-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3be2-218">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span><span class="sxs-lookup"><span data-stu-id="c3be2-218">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="c3be2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3be2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3be2-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c3be2-220">Additional resources</span></span>

* [<span data-ttu-id="c3be2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3be2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c3be2-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3be2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nexonia-tutorial/tutorial_general_01.png
[2]: ./media/nexonia-tutorial/tutorial_general_02.png
[3]: ./media/nexonia-tutorial/tutorial_general_03.png
[4]: ./media/nexonia-tutorial/tutorial_general_04.png

[100]: ./media/nexonia-tutorial/tutorial_general_100.png

[200]: ./media/nexonia-tutorial/tutorial_general_200.png
[201]: ./media/nexonia-tutorial/tutorial_general_201.png
[202]: ./media/nexonia-tutorial/tutorial_general_202.png
[203]: ./media/nexonia-tutorial/tutorial_general_203.png

