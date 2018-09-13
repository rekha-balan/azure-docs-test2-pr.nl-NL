---
title: 'Tutorial: Azure Active Directory integration with Dynamic Signal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dynamic Signal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 863f7340-b065-4f59-b092-daa67da6f703
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2018
ms.author: jeedes
ms.openlocfilehash: 2ca787be6d3697c84b8eeef637af8a14b190b428
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965544"
---
# <a name="tutorial-azure-active-directory-integration-with-dynamic-signal"></a><span data-ttu-id="9e3cf-103">Tutorial: Azure Active Directory integration with Dynamic Signal</span><span class="sxs-lookup"><span data-stu-id="9e3cf-103">Tutorial: Azure Active Directory integration with Dynamic Signal</span></span>

<span data-ttu-id="9e3cf-104">In this tutorial, you learn how to integrate Dynamic Signal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-104">In this tutorial, you learn how to integrate Dynamic Signal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e3cf-105">Integrating Dynamic Signal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-105">Integrating Dynamic Signal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e3cf-106">You can control in Azure AD who has access to Dynamic Signal.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-106">You can control in Azure AD who has access to Dynamic Signal.</span></span>
- <span data-ttu-id="9e3cf-107">You can enable your users to automatically get signed-on to Dynamic Signal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-107">You can enable your users to automatically get signed-on to Dynamic Signal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9e3cf-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9e3cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e3cf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9e3cf-110">Prerequisites</span></span>

<span data-ttu-id="9e3cf-111">To configure Azure AD integration with Dynamic Signal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-111">To configure Azure AD integration with Dynamic Signal, you need the following items:</span></span>

- <span data-ttu-id="9e3cf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9e3cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e3cf-113">A Dynamic Signal single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9e3cf-113">A Dynamic Signal single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e3cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e3cf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e3cf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e3cf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e3cf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9e3cf-118">Scenario description</span></span>
<span data-ttu-id="9e3cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e3cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e3cf-121">Adding Dynamic Signal from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e3cf-121">Adding Dynamic Signal from the gallery</span></span>
1. <span data-ttu-id="9e3cf-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e3cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dynamic-signal-from-the-gallery"></a><span data-ttu-id="9e3cf-123">Adding Dynamic Signal from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e3cf-123">Adding Dynamic Signal from the gallery</span></span>
<span data-ttu-id="9e3cf-124">To configure the integration of Dynamic Signal into Azure AD, you need to add Dynamic Signal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-124">To configure the integration of Dynamic Signal into Azure AD, you need to add Dynamic Signal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e3cf-125">**To add Dynamic Signal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e3cf-125">**To add Dynamic Signal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e3cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9e3cf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e3cf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="9e3cf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9e3cf-133">In the search box, type **Dynamic Signal**, select **Dynamic Signal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-133">In the search box, type **Dynamic Signal**, select **Dynamic Signal** from result panel then click **Add** button to add the application.</span></span>

    ![Dynamic Signal in the results list](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9e3cf-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e3cf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9e3cf-136">In this section, you configure and test Azure AD single sign-on with Dynamic Signal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e3cf-136">In this section, you configure and test Azure AD single sign-on with Dynamic Signal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e3cf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dynamic Signal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dynamic Signal is to a user in Azure AD.</span></span> <span data-ttu-id="9e3cf-138">In other words, a link relationship between an Azure AD user and the related user in Dynamic Signal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-138">In other words, a link relationship between an Azure AD user and the related user in Dynamic Signal needs to be established.</span></span>

<span data-ttu-id="9e3cf-139">To configure and test Azure AD single sign-on with Dynamic Signal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-139">To configure and test Azure AD single sign-on with Dynamic Signal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e3cf-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9e3cf-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9e3cf-142">**[Create a Dynamic Signal test user](#create-a-dynamic-signal-test-user)** - to have a counterpart of Britta Simon in Dynamic Signal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-142">**[Create a Dynamic Signal test user](#create-a-dynamic-signal-test-user)** - to have a counterpart of Britta Simon in Dynamic Signal that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9e3cf-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9e3cf-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9e3cf-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e3cf-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9e3cf-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dynamic Signal application.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dynamic Signal application.</span></span>

<span data-ttu-id="9e3cf-147">**To configure Azure AD single sign-on with Dynamic Signal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e3cf-147">**To configure Azure AD single sign-on with Dynamic Signal, perform the following steps:**</span></span>

1. <span data-ttu-id="9e3cf-148">In the Azure portal, on the **Dynamic Signal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-148">In the Azure portal, on the **Dynamic Signal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="9e3cf-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_samlbase.png)

1. <span data-ttu-id="9e3cf-152">On the **Dynamic Signal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-152">On the **Dynamic Signal Domain and URLs** section, perform the following steps:</span></span>
 
    ![Dynamic Signal Domain and URLs single sign-on information](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_url.png)

    <span data-ttu-id="9e3cf-154">a.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-154">a.</span></span> <span data-ttu-id="9e3cf-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`</span><span class="sxs-lookup"><span data-stu-id="9e3cf-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`</span></span>

    <span data-ttu-id="9e3cf-156">b.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-156">b.</span></span> <span data-ttu-id="9e3cf-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`</span><span class="sxs-lookup"><span data-stu-id="9e3cf-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`</span></span>

    <span data-ttu-id="9e3cf-158">c.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-158">c.</span></span> <span data-ttu-id="9e3cf-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com/User/SsoResponse`</span><span class="sxs-lookup"><span data-stu-id="9e3cf-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com/User/SsoResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e3cf-160">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-160">These values are not real.</span></span> <span data-ttu-id="9e3cf-161">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-161">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9e3cf-162">Contact [Dynamic Signal Client support team](mailto:support@dynamicsignal.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-162">Contact [Dynamic Signal Client support team](mailto:support@dynamicsignal.com) to get these values.</span></span> 

1. <span data-ttu-id="9e3cf-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_certificate.png) 

1. <span data-ttu-id="9e3cf-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/dynamicsignal-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="9e3cf-167">On the **Dynamic Signal Configuration** section, click **Configure Dynamic Signal** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-167">On the **Dynamic Signal Configuration** section, click **Configure Dynamic Signal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e3cf-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9e3cf-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Dynamic Signal Configuration](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_configure.png) 

1. <span data-ttu-id="9e3cf-170">To configure single sign-on on **Dynamic Signal** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Dynamic Signal support team](mailto:support@dynamicsignal.com).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-170">To configure single sign-on on **Dynamic Signal** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Dynamic Signal support team](mailto:support@dynamicsignal.com).</span></span> <span data-ttu-id="9e3cf-171">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9e3cf-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e3cf-172">Create an Azure AD test user</span></span>

<span data-ttu-id="9e3cf-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9e3cf-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e3cf-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e3cf-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/dynamicsignal-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9e3cf-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/dynamicsignal-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9e3cf-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/dynamicsignal-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9e3cf-182">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e3cf-182">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/dynamicsignal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9e3cf-184">a.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-184">a.</span></span> <span data-ttu-id="9e3cf-185">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-185">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e3cf-186">b.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-186">b.</span></span> <span data-ttu-id="9e3cf-187">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-187">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9e3cf-188">c.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-188">c.</span></span> <span data-ttu-id="9e3cf-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9e3cf-190">d.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-190">d.</span></span> <span data-ttu-id="9e3cf-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-191">Click **Create**.</span></span>
 
### <a name="create-a-dynamic-signal-test-user"></a><span data-ttu-id="9e3cf-192">Create a Dynamic Signal test user</span><span class="sxs-lookup"><span data-stu-id="9e3cf-192">Create a Dynamic Signal test user</span></span>

<span data-ttu-id="9e3cf-193">The objective of this section is to create a user called Britta Simon in Dynamic Signal.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-193">The objective of this section is to create a user called Britta Simon in Dynamic Signal.</span></span> <span data-ttu-id="9e3cf-194">Dynamic Signal supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-194">Dynamic Signal supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9e3cf-195">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-195">There is no action item for you in this section.</span></span> <span data-ttu-id="9e3cf-196">A new user is created during an attempt to access Dynamic Signal if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-196">A new user is created during an attempt to access Dynamic Signal if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="9e3cf-197">If you need to create a user manually, contact [Dynamic Signal support team](mailto:support@dynamicsignal.com).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-197">If you need to create a user manually, contact [Dynamic Signal support team](mailto:support@dynamicsignal.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9e3cf-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e3cf-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="9e3cf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dynamic Signal.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dynamic Signal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9e3cf-201">**To assign Britta Simon to Dynamic Signal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e3cf-201">**To assign Britta Simon to Dynamic Signal, perform the following steps:**</span></span>

1. <span data-ttu-id="9e3cf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9e3cf-204">In the applications list, select **Dynamic Signal**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-204">In the applications list, select **Dynamic Signal**.</span></span>

    ![The Dynamic Signal link in the Applications list](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_app.png)  

1. <span data-ttu-id="9e3cf-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9e3cf-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-208">Click **Add** button.</span></span> <span data-ttu-id="9e3cf-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9e3cf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9e3cf-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9e3cf-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9e3cf-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e3cf-214">Test single sign-on</span></span>

<span data-ttu-id="9e3cf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e3cf-216">When you click the Dynamic Signal tile in the Access Panel, you should get automatically signed-on to your Dynamic Signal application.</span><span class="sxs-lookup"><span data-stu-id="9e3cf-216">When you click the Dynamic Signal tile in the Access Panel, you should get automatically signed-on to your Dynamic Signal application.</span></span>
<span data-ttu-id="9e3cf-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e3cf-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e3cf-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9e3cf-218">Additional resources</span></span>

* [<span data-ttu-id="9e3cf-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e3cf-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9e3cf-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e3cf-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dynamicsignal-tutorial/tutorial_general_01.png
[2]: ./media/dynamicsignal-tutorial/tutorial_general_02.png
[3]: ./media/dynamicsignal-tutorial/tutorial_general_03.png
[4]: ./media/dynamicsignal-tutorial/tutorial_general_04.png

[100]: ./media/dynamicsignal-tutorial/tutorial_general_100.png

[200]: ./media/dynamicsignal-tutorial/tutorial_general_200.png
[201]: ./media/dynamicsignal-tutorial/tutorial_general_201.png
[202]: ./media/dynamicsignal-tutorial/tutorial_general_202.png
[203]: ./media/dynamicsignal-tutorial/tutorial_general_203.png

