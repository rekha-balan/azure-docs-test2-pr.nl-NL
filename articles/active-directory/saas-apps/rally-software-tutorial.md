---
title: 'Tutorial: Azure Active Directory integration with Rally Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 2bb9df9fe0cb20cdd50d7ba716ee5cba562f3e1b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871474"
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="dbe81-103">Tutorial: Azure Active Directory integration with Rally Software</span><span class="sxs-lookup"><span data-stu-id="dbe81-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="dbe81-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbe81-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbe81-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dbe81-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dbe81-106">You can control in Azure AD who has access to Rally Software.</span><span class="sxs-lookup"><span data-stu-id="dbe81-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="dbe81-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dbe81-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dbe81-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dbe81-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dbe81-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dbe81-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbe81-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dbe81-110">Prerequisites</span></span>

<span data-ttu-id="dbe81-111">To configure Azure AD integration with Rally Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dbe81-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="dbe81-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dbe81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbe81-113">A Rally Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dbe81-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbe81-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dbe81-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbe81-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dbe81-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbe81-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dbe81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbe81-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbe81-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbe81-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dbe81-118">Scenario description</span></span>
<span data-ttu-id="dbe81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dbe81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbe81-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dbe81-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbe81-121">Adding Rally Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="dbe81-121">Adding Rally Software from the gallery</span></span>
1. <span data-ttu-id="dbe81-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dbe81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="dbe81-123">Adding Rally Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="dbe81-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="dbe81-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dbe81-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dbe81-125">**To add Rally Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dbe81-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dbe81-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dbe81-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="dbe81-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dbe81-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="dbe81-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dbe81-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="dbe81-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dbe81-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software in the results list](./media/rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dbe81-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dbe81-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dbe81-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dbe81-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dbe81-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbe81-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="dbe81-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dbe81-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="dbe81-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="dbe81-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dbe81-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dbe81-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dbe81-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dbe81-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dbe81-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbe81-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dbe81-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dbe81-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="dbe81-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dbe81-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dbe81-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dbe81-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dbe81-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dbe81-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dbe81-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span><span class="sxs-lookup"><span data-stu-id="dbe81-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="dbe81-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dbe81-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="dbe81-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="dbe81-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dbe81-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

1. <span data-ttu-id="dbe81-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbe81-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Rally Software Domain and URLs single sign-on information](./media/rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="dbe81-155">a.</span><span class="sxs-lookup"><span data-stu-id="dbe81-155">a.</span></span> <span data-ttu-id="dbe81-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="dbe81-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="dbe81-157">b.</span><span class="sxs-lookup"><span data-stu-id="dbe81-157">b.</span></span> <span data-ttu-id="dbe81-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="dbe81-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dbe81-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="dbe81-159">These values are not real.</span></span> <span data-ttu-id="dbe81-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="dbe81-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dbe81-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="dbe81-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


1. <span data-ttu-id="dbe81-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dbe81-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

1. <span data-ttu-id="dbe81-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dbe81-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/rally-software-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="dbe81-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dbe81-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dbe81-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="dbe81-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Rally Software Configuration](./media/rally-software-tutorial/tutorial_rallysoftware_configure.png) 

1. <span data-ttu-id="dbe81-169">Log in to your **Rally Software** tenant.</span><span class="sxs-lookup"><span data-stu-id="dbe81-169">Log in to your **Rally Software** tenant.</span></span>

1. <span data-ttu-id="dbe81-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="dbe81-171">![Subscription](./media/rally-software-tutorial/ic769531.png "Subscription")</span><span class="sxs-lookup"><span data-stu-id="dbe81-171">![Subscription](./media/rally-software-tutorial/ic769531.png "Subscription")</span></span>

1. <span data-ttu-id="dbe81-172">Click the **Action** button.</span><span class="sxs-lookup"><span data-stu-id="dbe81-172">Click the **Action** button.</span></span> <span data-ttu-id="dbe81-173">Select **Edit Subscription** at the top right side of the toolbar.</span><span class="sxs-lookup"><span data-stu-id="dbe81-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

1. <span data-ttu-id="dbe81-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span><span class="sxs-lookup"><span data-stu-id="dbe81-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="dbe81-175">![Authentication](./media/rally-software-tutorial/ic769542.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="dbe81-175">![Authentication](./media/rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="dbe81-176">a.</span><span class="sxs-lookup"><span data-stu-id="dbe81-176">a.</span></span> <span data-ttu-id="dbe81-177">Select **Rally or SSO authentication** from Authentication dropdown.</span><span class="sxs-lookup"><span data-stu-id="dbe81-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="dbe81-178">b.</span><span class="sxs-lookup"><span data-stu-id="dbe81-178">b.</span></span> <span data-ttu-id="dbe81-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dbe81-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="dbe81-180">c.</span><span class="sxs-lookup"><span data-stu-id="dbe81-180">c.</span></span> <span data-ttu-id="dbe81-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dbe81-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="dbe81-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dbe81-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dbe81-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dbe81-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dbe81-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbe81-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dbe81-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dbe81-185">Create an Azure AD test user</span></span>

<span data-ttu-id="dbe81-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbe81-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="dbe81-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dbe81-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dbe81-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="dbe81-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/rally-software-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="dbe81-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/rally-software-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="dbe81-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dbe81-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/rally-software-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="dbe81-195">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbe81-195">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dbe81-197">a.</span><span class="sxs-lookup"><span data-stu-id="dbe81-197">a.</span></span> <span data-ttu-id="dbe81-198">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbe81-199">b.</span><span class="sxs-lookup"><span data-stu-id="dbe81-199">b.</span></span> <span data-ttu-id="dbe81-200">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbe81-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dbe81-201">c.</span><span class="sxs-lookup"><span data-stu-id="dbe81-201">c.</span></span> <span data-ttu-id="dbe81-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="dbe81-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dbe81-203">d.</span><span class="sxs-lookup"><span data-stu-id="dbe81-203">d.</span></span> <span data-ttu-id="dbe81-204">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="dbe81-205">Create a Rally Software test user</span><span class="sxs-lookup"><span data-stu-id="dbe81-205">Create a Rally Software test user</span></span>

<span data-ttu-id="dbe81-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="dbe81-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="dbe81-207">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dbe81-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="dbe81-208">Log in to your Rally Software tenant.</span><span class="sxs-lookup"><span data-stu-id="dbe81-208">Log in to your Rally Software tenant.</span></span>

1. <span data-ttu-id="dbe81-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="dbe81-210">![Users](./media/rally-software-tutorial/ic781039.png "Users")</span><span class="sxs-lookup"><span data-stu-id="dbe81-210">![Users](./media/rally-software-tutorial/ic781039.png "Users")</span></span>

1. <span data-ttu-id="dbe81-211">Type the name in the New User textbox, and then click **Add with Details**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

1. <span data-ttu-id="dbe81-212">In the **Create User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dbe81-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dbe81-213">![Create User](./media/rally-software-tutorial/ic781040.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="dbe81-213">![Create User](./media/rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="dbe81-214">a.</span><span class="sxs-lookup"><span data-stu-id="dbe81-214">a.</span></span> <span data-ttu-id="dbe81-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="dbe81-216">b.</span><span class="sxs-lookup"><span data-stu-id="dbe81-216">b.</span></span> <span data-ttu-id="dbe81-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="dbe81-218">c.</span><span class="sxs-lookup"><span data-stu-id="dbe81-218">c.</span></span> <span data-ttu-id="dbe81-219">In **First Name** text box, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="dbe81-220">d.</span><span class="sxs-lookup"><span data-stu-id="dbe81-220">d.</span></span> <span data-ttu-id="dbe81-221">In **Last Name** text box, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="dbe81-222">e.</span><span class="sxs-lookup"><span data-stu-id="dbe81-222">e.</span></span> <span data-ttu-id="dbe81-223">Click **Save & Close**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dbe81-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="dbe81-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dbe81-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dbe81-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="dbe81-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span><span class="sxs-lookup"><span data-stu-id="dbe81-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Assign the user role][200] 

<span data-ttu-id="dbe81-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dbe81-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="dbe81-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="dbe81-231">In the applications list, select **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-231">In the applications list, select **Rally Software**.</span></span>

    ![The Rally Software link in the Applications list](./media/rally-software-tutorial/tutorial_rallysoftware_app.png)  

1. <span data-ttu-id="dbe81-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dbe81-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="dbe81-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dbe81-235">Click **Add** button.</span></span> <span data-ttu-id="dbe81-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dbe81-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="dbe81-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dbe81-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="dbe81-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dbe81-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="dbe81-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dbe81-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dbe81-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dbe81-241">Test single sign-on</span></span>

<span data-ttu-id="dbe81-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dbe81-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dbe81-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span><span class="sxs-lookup"><span data-stu-id="dbe81-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbe81-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dbe81-244">Additional resources</span></span>

* [<span data-ttu-id="dbe81-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbe81-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dbe81-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbe81-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/rally-software-tutorial/tutorial_general_01.png
[2]: ./media/rally-software-tutorial/tutorial_general_02.png
[3]: ./media/rally-software-tutorial/tutorial_general_03.png
[4]: ./media/rally-software-tutorial/tutorial_general_04.png

[100]: ./media/rally-software-tutorial/tutorial_general_100.png

[200]: ./media/rally-software-tutorial/tutorial_general_200.png
[201]: ./media/rally-software-tutorial/tutorial_general_201.png
[202]: ./media/rally-software-tutorial/tutorial_general_202.png
[203]: ./media/rally-software-tutorial/tutorial_general_203.png

