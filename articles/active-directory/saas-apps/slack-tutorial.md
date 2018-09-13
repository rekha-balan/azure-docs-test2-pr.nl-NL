---
title: 'Tutorial: Azure Active Directory integration with Slack | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Slack.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: b742f3eb9124093bcf0c3c912bbae0367cdcce56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871705"
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="8a978-103">Tutorial: Azure Active Directory integration with Slack</span><span class="sxs-lookup"><span data-stu-id="8a978-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="8a978-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a978-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a978-105">Integrating Slack with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8a978-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a978-106">You can control in Azure AD who has access to Slack</span><span class="sxs-lookup"><span data-stu-id="8a978-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="8a978-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8a978-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a978-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8a978-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a978-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8a978-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a978-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a978-110">Prerequisites</span></span>

<span data-ttu-id="8a978-111">To configure Azure AD integration with Slack, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8a978-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="8a978-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8a978-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a978-113">A Slack single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8a978-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a978-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8a978-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a978-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8a978-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a978-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8a978-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a978-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a978-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a978-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8a978-118">Scenario description</span></span>
<span data-ttu-id="8a978-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8a978-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a978-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a978-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a978-121">Adding Slack from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a978-121">Adding Slack from the gallery</span></span>
1. <span data-ttu-id="8a978-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a978-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="8a978-123">Adding Slack from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a978-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="8a978-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8a978-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a978-125">**To add Slack from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a978-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a978-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8a978-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8a978-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8a978-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a978-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a978-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8a978-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8a978-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8a978-133">In the search box, type **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8a978-133">In the search box, type **Slack**.</span></span>

    ![Creating an Azure AD test user](./media/slack-tutorial/tutorial_slack_search.png)

1. <span data-ttu-id="8a978-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8a978-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a978-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a978-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a978-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8a978-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a978-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a978-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="8a978-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8a978-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="8a978-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8a978-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a978-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a978-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a978-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8a978-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8a978-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a978-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8a978-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8a978-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8a978-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a978-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8a978-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8a978-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a978-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a978-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a978-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span><span class="sxs-lookup"><span data-stu-id="8a978-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="8a978-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a978-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8a978-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8a978-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8a978-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a978-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_samlbase.png)

1. <span data-ttu-id="8a978-155">On the **Slack Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a978-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="8a978-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a978-157">a.</span></span> <span data-ttu-id="8a978-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="8a978-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="8a978-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a978-159">b.</span></span> <span data-ttu-id="8a978-160">In the **Identifier** textbox, update the value with the Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="8a978-160">In the **Identifier** textbox, update the value with the Sign On URL.</span></span> <span data-ttu-id="8a978-161">This is your workspace domain.</span><span class="sxs-lookup"><span data-stu-id="8a978-161">This is your workspace domain.</span></span> <span data-ttu-id="8a978-162">For example: `https://contoso.slack.com`</span><span class="sxs-lookup"><span data-stu-id="8a978-162">For example: `https://contoso.slack.com`</span></span>

1. <span data-ttu-id="8a978-163">Slack application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="8a978-163">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8a978-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="8a978-164">Configure the following claims for this application.</span></span> <span data-ttu-id="8a978-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="8a978-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8a978-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="8a978-166">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="8a978-168">If you have users who’s assigned **email address** is not on a Office365 license, the **User.Email** claim will not appear in the SAML Token.</span><span class="sxs-lookup"><span data-stu-id="8a978-168">If you have users who’s assigned **email address** is not on a Office365 license, the **User.Email** claim will not appear in the SAML Token.</span></span> <span data-ttu-id="8a978-169">In these cases, we suggest using **user.userprincipalname** as the **User.Email** attribute value to map as **Unique Identifier** instead.</span><span class="sxs-lookup"><span data-stu-id="8a978-169">In these cases, we suggest using **user.userprincipalname** as the **User.Email** attribute value to map as **Unique Identifier** instead.</span></span>

1. <span data-ttu-id="8a978-170">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a978-170">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="8a978-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="8a978-171">Attribute Name</span></span> | <span data-ttu-id="8a978-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="8a978-172">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8a978-173">first_name</span><span class="sxs-lookup"><span data-stu-id="8a978-173">first_name</span></span> | <span data-ttu-id="8a978-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8a978-174">user.givenname</span></span> |
    | <span data-ttu-id="8a978-175">last_name</span><span class="sxs-lookup"><span data-stu-id="8a978-175">last_name</span></span> | <span data-ttu-id="8a978-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="8a978-176">user.surname</span></span> |
    | <span data-ttu-id="8a978-177">User.Email</span><span class="sxs-lookup"><span data-stu-id="8a978-177">User.Email</span></span> | <span data-ttu-id="8a978-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="8a978-178">user.mail</span></span> |  
    | <span data-ttu-id="8a978-179">User.Username</span><span class="sxs-lookup"><span data-stu-id="8a978-179">User.Username</span></span> | <span data-ttu-id="8a978-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8a978-180">user.userprincipalname</span></span> |

    <span data-ttu-id="8a978-181">a.</span><span class="sxs-lookup"><span data-stu-id="8a978-181">a.</span></span> <span data-ttu-id="8a978-182">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a978-182">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="8a978-184">a.</span><span class="sxs-lookup"><span data-stu-id="8a978-184">a.</span></span> <span data-ttu-id="8a978-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8a978-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="8a978-186">b.</span><span class="sxs-lookup"><span data-stu-id="8a978-186">b.</span></span> <span data-ttu-id="8a978-187">From the **Value** list, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8a978-187">From the **Value** list, select the attribute value shown for that row.</span></span>

    <span data-ttu-id="8a978-188">c.</span><span class="sxs-lookup"><span data-stu-id="8a978-188">c.</span></span> <span data-ttu-id="8a978-189">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="8a978-189">Leave the **Namespace** blank.</span></span>

    <span data-ttu-id="8a978-190">d.</span><span class="sxs-lookup"><span data-stu-id="8a978-190">d.</span></span> <span data-ttu-id="8a978-191">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="8a978-191">Click **OK**</span></span>

1. <span data-ttu-id="8a978-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8a978-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_certificate.png)

1. <span data-ttu-id="8a978-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8a978-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8a978-196">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8a978-196">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8a978-197">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8a978-197">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_configure.png)

1. <span data-ttu-id="8a978-199">In a different web browser window, log in to your Slack company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8a978-199">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

1. <span data-ttu-id="8a978-200">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span><span class="sxs-lookup"><span data-stu-id="8a978-200">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Configure Single Sign-On On App Side](./media/slack-tutorial/tutorial_slack_001.png)

1. <span data-ttu-id="8a978-202">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span><span class="sxs-lookup"><span data-stu-id="8a978-202">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

    ![Configure Single Sign-On On App Side](./media/slack-tutorial/tutorial_slack_002.png)

1. <span data-ttu-id="8a978-204">On the **SAML Authentication Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a978-204">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](./media/slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="8a978-206">a.</span><span class="sxs-lookup"><span data-stu-id="8a978-206">a.</span></span>  <span data-ttu-id="8a978-207">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a978-207">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8a978-208">b.</span><span class="sxs-lookup"><span data-stu-id="8a978-208">b.</span></span>  <span data-ttu-id="8a978-209">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a978-209">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8a978-210">c.</span><span class="sxs-lookup"><span data-stu-id="8a978-210">c.</span></span>  <span data-ttu-id="8a978-211">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="8a978-211">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="8a978-212">d.</span><span class="sxs-lookup"><span data-stu-id="8a978-212">d.</span></span> <span data-ttu-id="8a978-213">Configure the above three settings as appropriate for your Slack team.</span><span class="sxs-lookup"><span data-stu-id="8a978-213">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="8a978-214">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span><span class="sxs-lookup"><span data-stu-id="8a978-214">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="8a978-215">e.</span><span class="sxs-lookup"><span data-stu-id="8a978-215">e.</span></span>  <span data-ttu-id="8a978-216">Click **Save Configuration**.</span><span class="sxs-lookup"><span data-stu-id="8a978-216">Click **Save Configuration**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a978-217">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a978-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a978-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a978-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8a978-220">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a978-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a978-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8a978-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/slack-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8a978-223">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8a978-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/slack-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8a978-225">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8a978-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/slack-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="8a978-227">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a978-227">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/slack-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8a978-229">a.</span><span class="sxs-lookup"><span data-stu-id="8a978-229">a.</span></span> <span data-ttu-id="8a978-230">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a978-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a978-231">b.</span><span class="sxs-lookup"><span data-stu-id="8a978-231">b.</span></span> <span data-ttu-id="8a978-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a978-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a978-233">c.</span><span class="sxs-lookup"><span data-stu-id="8a978-233">c.</span></span> <span data-ttu-id="8a978-234">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8a978-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a978-235">d.</span><span class="sxs-lookup"><span data-stu-id="8a978-235">d.</span></span> <span data-ttu-id="8a978-236">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a978-236">Click **Create**.</span></span>

### <a name="creating-a-slack-test-user"></a><span data-ttu-id="8a978-237">Creating a Slack test user</span><span class="sxs-lookup"><span data-stu-id="8a978-237">Creating a Slack test user</span></span>

<span data-ttu-id="8a978-238">The objective of this section is to create a user called Britta Simon in Slack.</span><span class="sxs-lookup"><span data-stu-id="8a978-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="8a978-239">Slack supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="8a978-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="8a978-240">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="8a978-240">There is no action item for you in this section.</span></span> <span data-ttu-id="8a978-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="8a978-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span> <span data-ttu-id="8a978-242">Slack also supports automatic user provisioning, you can find more details [here](slack-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="8a978-242">Slack also supports automatic user provisioning, you can find more details [here](slack-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="8a978-243">If you need to create a user manually, you need to contact [Slack support team](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="8a978-243">If you need to create a user manually, you need to contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a978-244">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a978-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a978-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span><span class="sxs-lookup"><span data-stu-id="8a978-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Assign User][200]

<span data-ttu-id="8a978-247">**To assign Britta Simon to Slack, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a978-247">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8a978-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a978-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8a978-250">In the applications list, select **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8a978-250">In the applications list, select **Slack**.</span></span>

    ![Configure Single Sign-On](./media/slack-tutorial/tutorial_slack_app.png) 

1. <span data-ttu-id="8a978-252">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8a978-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8a978-254">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8a978-254">Click **Add** button.</span></span> <span data-ttu-id="8a978-255">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a978-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8a978-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8a978-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8a978-258">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a978-258">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8a978-259">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a978-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a978-260">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a978-260">Testing single sign-on</span></span>

<span data-ttu-id="8a978-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8a978-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a978-262">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span><span class="sxs-lookup"><span data-stu-id="8a978-262">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a978-263">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8a978-263">Additional resources</span></span>

* [<span data-ttu-id="8a978-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a978-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8a978-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a978-265">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="8a978-266">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="8a978-266">Configure User Provisioning</span></span>](slack-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/slack-tutorial/tutorial_general_01.png
[2]: ./media/slack-tutorial/tutorial_general_02.png
[3]: ./media/slack-tutorial/tutorial_general_03.png
[4]: ./media/slack-tutorial/tutorial_general_04.png

[100]: ./media/slack-tutorial/tutorial_general_100.png

[200]: ./media/slack-tutorial/tutorial_general_200.png
[201]: ./media/slack-tutorial/tutorial_general_201.png
[202]: ./media/slack-tutorial/tutorial_general_202.png
[203]: ./media/slack-tutorial/tutorial_general_203.png
