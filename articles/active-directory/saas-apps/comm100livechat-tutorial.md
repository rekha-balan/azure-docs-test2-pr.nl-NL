---
title: 'Tutorial: Azure Active Directory integration with Comm100 Live Chat | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Comm100 Live Chat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0340d7f3-ab54-49ef-b77c-62a0efd5d49c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2018
ms.author: jeedes
ms.openlocfilehash: b85162c8392e8ecdb08a3ed04ff5b9de835808a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855864"
---
# <a name="tutorial-azure-active-directory-integration-with-comm100-live-chat"></a><span data-ttu-id="fee3a-103">Tutorial: Azure Active Directory integration with Comm100 Live Chat</span><span class="sxs-lookup"><span data-stu-id="fee3a-103">Tutorial: Azure Active Directory integration with Comm100 Live Chat</span></span>

<span data-ttu-id="fee3a-104">In this tutorial, you learn how to integrate Comm100 Live Chat with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fee3a-104">In this tutorial, you learn how to integrate Comm100 Live Chat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fee3a-105">Integrating Comm100 Live Chat with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fee3a-105">Integrating Comm100 Live Chat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fee3a-106">You can control in Azure AD who has access to Comm100 Live Chat.</span><span class="sxs-lookup"><span data-stu-id="fee3a-106">You can control in Azure AD who has access to Comm100 Live Chat.</span></span>
- <span data-ttu-id="fee3a-107">You can enable your users to automatically get signed-on to Comm100 Live Chat (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="fee3a-107">You can enable your users to automatically get signed-on to Comm100 Live Chat (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fee3a-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fee3a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fee3a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fee3a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee3a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fee3a-110">Prerequisites</span></span>

<span data-ttu-id="fee3a-111">To configure Azure AD integration with Comm100 Live Chat, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fee3a-111">To configure Azure AD integration with Comm100 Live Chat, you need the following items:</span></span>

- <span data-ttu-id="fee3a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fee3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fee3a-113">A Comm100 Live Chat single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fee3a-113">A Comm100 Live Chat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fee3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fee3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fee3a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fee3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fee3a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fee3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fee3a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fee3a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fee3a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fee3a-118">Scenario description</span></span>
<span data-ttu-id="fee3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fee3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fee3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fee3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fee3a-121">Adding Comm100 Live Chat from the gallery</span><span class="sxs-lookup"><span data-stu-id="fee3a-121">Adding Comm100 Live Chat from the gallery</span></span>
2. <span data-ttu-id="fee3a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fee3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-comm100-live-chat-from-the-gallery"></a><span data-ttu-id="fee3a-123">Adding Comm100 Live Chat from the gallery</span><span class="sxs-lookup"><span data-stu-id="fee3a-123">Adding Comm100 Live Chat from the gallery</span></span>
<span data-ttu-id="fee3a-124">To configure the integration of Comm100 Live Chat into Azure AD, you need to add Comm100 Live Chat from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fee3a-124">To configure the integration of Comm100 Live Chat into Azure AD, you need to add Comm100 Live Chat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fee3a-125">**To add Comm100 Live Chat from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fee3a-125">**To add Comm100 Live Chat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fee3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fee3a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="fee3a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fee3a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="fee3a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fee3a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="fee3a-133">In the search box, type **Comm100 Live Chat**, select **Comm100 Live Chat** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fee3a-133">In the search box, type **Comm100 Live Chat**, select **Comm100 Live Chat** from result panel then click **Add** button to add the application.</span></span>

    ![Comm100 Live Chat in the results list](./media/comm100livechat-tutorial/tutorial_comm100livechat_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fee3a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fee3a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fee3a-136">In this section, you configure and test Azure AD single sign-on with Comm100 Live Chat based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fee3a-136">In this section, you configure and test Azure AD single sign-on with Comm100 Live Chat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fee3a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Comm100 Live Chat is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fee3a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Comm100 Live Chat is to a user in Azure AD.</span></span> <span data-ttu-id="fee3a-138">In other words, a link relationship between an Azure AD user and the related user in Comm100 Live Chat needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fee3a-138">In other words, a link relationship between an Azure AD user and the related user in Comm100 Live Chat needs to be established.</span></span>

<span data-ttu-id="fee3a-139">To configure and test Azure AD single sign-on with Comm100 Live Chat, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fee3a-139">To configure and test Azure AD single sign-on with Comm100 Live Chat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fee3a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fee3a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fee3a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fee3a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fee3a-142">**[Create a Comm100 Live Chat test user](#create-a-comm100-live-chat-test-user)** - to have a counterpart of Britta Simon in Comm100 Live Chat that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fee3a-142">**[Create a Comm100 Live Chat test user](#create-a-comm100-live-chat-test-user)** - to have a counterpart of Britta Simon in Comm100 Live Chat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fee3a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fee3a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fee3a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fee3a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fee3a-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fee3a-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fee3a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Comm100 Live Chat application.</span><span class="sxs-lookup"><span data-stu-id="fee3a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Comm100 Live Chat application.</span></span>

<span data-ttu-id="fee3a-147">**To configure Azure AD single sign-on with Comm100 Live Chat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fee3a-147">**To configure Azure AD single sign-on with Comm100 Live Chat, perform the following steps:**</span></span>

1. <span data-ttu-id="fee3a-148">In the Azure portal, on the **Comm100 Live Chat** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-148">In the Azure portal, on the **Comm100 Live Chat** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="fee3a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fee3a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/comm100livechat-tutorial/tutorial_comm100livechat_samlbase.png)

3. <span data-ttu-id="fee3a-152">On the **Comm100 Live Chat Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fee3a-152">On the **Comm100 Live Chat Domain and URLs** section, perform the following steps:</span></span>

    ![Comm100 Live Chat Domain and URLs single sign-on information](./media/comm100livechat-tutorial/tutorial_comm100livechat_url.png)

    <span data-ttu-id="fee3a-154">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.comm100.com/AdminManage/LoginSSO.aspx?siteId=<SITEID>`</span><span class="sxs-lookup"><span data-stu-id="fee3a-154">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.comm100.com/AdminManage/LoginSSO.aspx?siteId=<SITEID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="fee3a-155">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="fee3a-155">The Sign-on URL value is not real.</span></span> <span data-ttu-id="fee3a-156">You will update the Sign-on URL value with the actual Sign-on URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="fee3a-156">You will update the Sign-on URL value with the actual Sign-on URL, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="fee3a-157">Comm100 Live Chat application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="fee3a-157">Comm100 Live Chat application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="fee3a-158">Configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="fee3a-158">Configure the following attributes  for this application.</span></span> <span data-ttu-id="fee3a-159">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="fee3a-159">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="fee3a-160">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="fee3a-160">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/comm100livechat-tutorial/tutorial_attribute_03.png)
    
5. <span data-ttu-id="fee3a-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fee3a-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    |  <span data-ttu-id="fee3a-163">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="fee3a-163">Attribute Name</span></span>  | <span data-ttu-id="fee3a-164">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="fee3a-164">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="fee3a-165">email</span><span class="sxs-lookup"><span data-stu-id="fee3a-165">email</span></span>    | <span data-ttu-id="fee3a-166">user.mail</span><span class="sxs-lookup"><span data-stu-id="fee3a-166">user.mail</span></span> |

    <span data-ttu-id="fee3a-167">a.</span><span class="sxs-lookup"><span data-stu-id="fee3a-167">a.</span></span> <span data-ttu-id="fee3a-168">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="fee3a-168">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/comm100livechat-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/comm100livechat-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="fee3a-171">b.</span><span class="sxs-lookup"><span data-stu-id="fee3a-171">b.</span></span> <span data-ttu-id="fee3a-172">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="fee3a-172">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="fee3a-173">c.</span><span class="sxs-lookup"><span data-stu-id="fee3a-173">c.</span></span> <span data-ttu-id="fee3a-174">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="fee3a-174">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="fee3a-175">d.</span><span class="sxs-lookup"><span data-stu-id="fee3a-175">d.</span></span> <span data-ttu-id="fee3a-176">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="fee3a-176">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="fee3a-177">e.</span><span class="sxs-lookup"><span data-stu-id="fee3a-177">e.</span></span> <span data-ttu-id="fee3a-178">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-178">Click **Ok**.</span></span>

6. <span data-ttu-id="fee3a-179">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fee3a-179">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/comm100livechat-tutorial/tutorial_comm100livechat_certificate.png) 

7. <span data-ttu-id="fee3a-181">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fee3a-181">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/comm100livechat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fee3a-183">On the **Comm100 Live Chat Configuration** section, click **Configure Comm100 Live Chat** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="fee3a-183">On the **Comm100 Live Chat Configuration** section, click **Configure Comm100 Live Chat** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fee3a-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="fee3a-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Comm100 Live Chat Configuration](./media/comm100livechat-tutorial/tutorial_comm100livechat_configure.png)

9. <span data-ttu-id="fee3a-186">In a different web browser window, login to Comm100 Live Chat as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="fee3a-186">In a different web browser window, login to Comm100 Live Chat as a Security Administrator.</span></span>

10. <span data-ttu-id="fee3a-187">On the top right side of the page, click **My Account**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-187">On the top right side of the page, click **My Account**.</span></span>

    ![Comm100 Live Chat myaccount](./media/comm100livechat-tutorial/tutorial_comm100livechat_account.png)

11. <span data-ttu-id="fee3a-189">From the left side of menu, click **Security** and then click **Agent Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-189">From the left side of menu, click **Security** and then click **Agent Single Sign-On**.</span></span>

    ![Comm100 Live Chat security](./media/comm100livechat-tutorial/tutorial_comm100livechat_security.png)

12. <span data-ttu-id="fee3a-191">On the **Agent Single Sign-On** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fee3a-191">On the **Agent Single Sign-On** page, perform the following steps:</span></span>

    ![Comm100 Live Chat security](./media/comm100livechat-tutorial/tutorial_comm100livechat_singlesignon.png)

    <span data-ttu-id="fee3a-193">a.</span><span class="sxs-lookup"><span data-stu-id="fee3a-193">a.</span></span> <span data-ttu-id="fee3a-194">Copy the first highlighted link and paste it in **Sign-on URL** textbox in **Comm100 Live Chat Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fee3a-194">Copy the first highlighted link and paste it in **Sign-on URL** textbox in **Comm100 Live Chat Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="fee3a-195">b.</span><span class="sxs-lookup"><span data-stu-id="fee3a-195">b.</span></span> <span data-ttu-id="fee3a-196">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fee3a-196">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="fee3a-197">c.</span><span class="sxs-lookup"><span data-stu-id="fee3a-197">c.</span></span> <span data-ttu-id="fee3a-198">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fee3a-198">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="fee3a-199">d.</span><span class="sxs-lookup"><span data-stu-id="fee3a-199">d.</span></span> <span data-ttu-id="fee3a-200">Click **Choose a File** to upload the base-64 encoded certificate that you have downloaded from the Azure portal, into the **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-200">Click **Choose a File** to upload the base-64 encoded certificate that you have downloaded from the Azure portal, into the **Certificate**.</span></span>

    <span data-ttu-id="fee3a-201">e.</span><span class="sxs-lookup"><span data-stu-id="fee3a-201">e.</span></span> <span data-ttu-id="fee3a-202">Click **Save Changes**</span><span class="sxs-lookup"><span data-stu-id="fee3a-202">Click **Save Changes**</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fee3a-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fee3a-203">Create an Azure AD test user</span></span>

<span data-ttu-id="fee3a-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fee3a-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="fee3a-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fee3a-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fee3a-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="fee3a-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/comm100livechat-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fee3a-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/comm100livechat-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fee3a-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fee3a-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/comm100livechat-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fee3a-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fee3a-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/comm100livechat-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fee3a-215">a.</span><span class="sxs-lookup"><span data-stu-id="fee3a-215">a.</span></span> <span data-ttu-id="fee3a-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fee3a-217">b.</span><span class="sxs-lookup"><span data-stu-id="fee3a-217">b.</span></span> <span data-ttu-id="fee3a-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fee3a-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fee3a-219">c.</span><span class="sxs-lookup"><span data-stu-id="fee3a-219">c.</span></span> <span data-ttu-id="fee3a-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="fee3a-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fee3a-221">d.</span><span class="sxs-lookup"><span data-stu-id="fee3a-221">d.</span></span> <span data-ttu-id="fee3a-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-222">Click **Create**.</span></span>
 
### <a name="create-a-comm100-live-chat-test-user"></a><span data-ttu-id="fee3a-223">Create a Comm100 Live Chat test user</span><span class="sxs-lookup"><span data-stu-id="fee3a-223">Create a Comm100 Live Chat test user</span></span>

<span data-ttu-id="fee3a-224">To enable Azure AD users to log in to Comm100 Live Chat, they must be provisioned into Comm100 Live Chat.</span><span class="sxs-lookup"><span data-stu-id="fee3a-224">To enable Azure AD users to log in to Comm100 Live Chat, they must be provisioned into Comm100 Live Chat.</span></span> <span data-ttu-id="fee3a-225">In Comm100 Live Chat, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="fee3a-225">In Comm100 Live Chat, provisioning is a manual task.</span></span>

<span data-ttu-id="fee3a-226">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fee3a-226">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fee3a-227">Log in to Comm100 Live Chat as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="fee3a-227">Log in to Comm100 Live Chat as a Security Administrator.</span></span>

2. <span data-ttu-id="fee3a-228">On the top right side of the page, click **My Account**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-228">On the top right side of the page, click **My Account**.</span></span>

    ![Comm100 Live Chat myaccount](./media/comm100livechat-tutorial/tutorial_comm100livechat_account.png)

3. <span data-ttu-id="fee3a-230">From the left side of menu, click **Agents** and then click **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-230">From the left side of menu, click **Agents** and then click **New Agent**.</span></span>

    ![Comm100 Live Chat agent](./media/comm100livechat-tutorial/tutorial_comm100livechat_agent.png)

4. <span data-ttu-id="fee3a-232">On the **New Agent** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fee3a-232">On the **New Agent** page, perform the following steps:</span></span>

    ![Comm100 Live Chat new agent](./media/comm100livechat-tutorial/tutorial_comm100livechat_newagent.png)

    <span data-ttu-id="fee3a-234">a.</span><span class="sxs-lookup"><span data-stu-id="fee3a-234">a.</span></span> <span data-ttu-id="fee3a-235">a.</span><span class="sxs-lookup"><span data-stu-id="fee3a-235">a.</span></span> <span data-ttu-id="fee3a-236">In **Email** text box, enter the email of user like **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-236">In **Email** text box, enter the email of user like **Brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="fee3a-237">b.</span><span class="sxs-lookup"><span data-stu-id="fee3a-237">b.</span></span> <span data-ttu-id="fee3a-238">In **First Name** text box, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-238">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="fee3a-239">c.</span><span class="sxs-lookup"><span data-stu-id="fee3a-239">c.</span></span> <span data-ttu-id="fee3a-240">In **Last Name** text box, enter the last name of user like **simon**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-240">In **Last Name** text box, enter the last name of user like **simon**.</span></span>

    <span data-ttu-id="fee3a-241">d.</span><span class="sxs-lookup"><span data-stu-id="fee3a-241">d.</span></span> <span data-ttu-id="fee3a-242">In the **Display Name** textbox, enter the display name of user like **Britta simon**</span><span class="sxs-lookup"><span data-stu-id="fee3a-242">In the **Display Name** textbox, enter the display name of user like **Britta simon**</span></span>

    <span data-ttu-id="fee3a-243">e.</span><span class="sxs-lookup"><span data-stu-id="fee3a-243">e.</span></span> <span data-ttu-id="fee3a-244">In the **Password** textbox, type your password.</span><span class="sxs-lookup"><span data-stu-id="fee3a-244">In the **Password** textbox, type your password.</span></span>

    <span data-ttu-id="fee3a-245">f.</span><span class="sxs-lookup"><span data-stu-id="fee3a-245">f.</span></span> <span data-ttu-id="fee3a-246">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-246">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fee3a-247">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fee3a-247">Assign the Azure AD test user</span></span>

<span data-ttu-id="fee3a-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Comm100 Live Chat.</span><span class="sxs-lookup"><span data-stu-id="fee3a-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Comm100 Live Chat.</span></span>

![Assign the user role][200] 

<span data-ttu-id="fee3a-250">**To assign Britta Simon to Comm100 Live Chat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fee3a-250">**To assign Britta Simon to Comm100 Live Chat, perform the following steps:**</span></span>

1. <span data-ttu-id="fee3a-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="fee3a-253">In the applications list, select **Comm100 Live Chat**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-253">In the applications list, select **Comm100 Live Chat**.</span></span>

    ![The Comm100 Live Chat link in the Applications list](./media/comm100livechat-tutorial/tutorial_comm100livechat_app.png)  

3. <span data-ttu-id="fee3a-255">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fee3a-255">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="fee3a-257">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fee3a-257">Click **Add** button.</span></span> <span data-ttu-id="fee3a-258">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fee3a-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="fee3a-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fee3a-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fee3a-261">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fee3a-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fee3a-262">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fee3a-262">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fee3a-263">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fee3a-263">Test single sign-on</span></span>

<span data-ttu-id="fee3a-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fee3a-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fee3a-265">When you click the Comm100 Live Chat tile in the Access Panel, you should get automatically signed-on to your Comm100 Live Chat application.</span><span class="sxs-lookup"><span data-stu-id="fee3a-265">When you click the Comm100 Live Chat tile in the Access Panel, you should get automatically signed-on to your Comm100 Live Chat application.</span></span>
<span data-ttu-id="fee3a-266">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fee3a-266">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fee3a-267">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fee3a-267">Additional resources</span></span>

* [<span data-ttu-id="fee3a-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fee3a-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fee3a-269">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fee3a-269">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/comm100livechat-tutorial/tutorial_general_01.png
[2]: ./media/comm100livechat-tutorial/tutorial_general_02.png
[3]: ./media/comm100livechat-tutorial/tutorial_general_03.png
[4]: ./media/comm100livechat-tutorial/tutorial_general_04.png

[100]: ./media/comm100livechat-tutorial/tutorial_general_100.png

[200]: ./media/comm100livechat-tutorial/tutorial_general_200.png
[201]: ./media/comm100livechat-tutorial/tutorial_general_201.png
[202]: ./media/comm100livechat-tutorial/tutorial_general_202.png
[203]: ./media/comm100livechat-tutorial/tutorial_general_203.png

