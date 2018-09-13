---
title: 'Tutorial: Azure Active Directory integration with OpsGenie | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 715035072ddc2ceb087d003dd5da5bc47572e9b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869460"
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="e7225-103">Tutorial: Azure Active Directory integration with OpsGenie</span><span class="sxs-lookup"><span data-stu-id="e7225-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="e7225-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7225-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7225-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e7225-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7225-106">You can control in Azure AD who has access to OpsGenie</span><span class="sxs-lookup"><span data-stu-id="e7225-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="e7225-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e7225-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7225-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e7225-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7225-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e7225-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7225-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e7225-110">Prerequisites</span></span>

<span data-ttu-id="e7225-111">To configure Azure AD integration with OpsGenie, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e7225-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="e7225-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e7225-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7225-113">A OpsGenie single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e7225-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7225-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e7225-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7225-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e7225-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7225-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e7225-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7225-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7225-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7225-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e7225-118">Scenario description</span></span>
<span data-ttu-id="e7225-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e7225-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7225-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e7225-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7225-121">Adding OpsGenie from the gallery</span><span class="sxs-lookup"><span data-stu-id="e7225-121">Adding OpsGenie from the gallery</span></span>
1. <span data-ttu-id="e7225-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e7225-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="e7225-123">Adding OpsGenie from the gallery</span><span class="sxs-lookup"><span data-stu-id="e7225-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="e7225-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e7225-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7225-125">**To add OpsGenie from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e7225-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7225-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e7225-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="e7225-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e7225-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7225-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e7225-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="e7225-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e7225-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="e7225-133">In the search box, type **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="e7225-133">In the search box, type **OpsGenie**.</span></span>

    ![Creating an Azure AD test user](./media/opsgenie-tutorial/tutorial_opsgenie_search.png)

1. <span data-ttu-id="e7225-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e7225-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7225-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e7225-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7225-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7225-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7225-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7225-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="e7225-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e7225-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="e7225-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e7225-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7225-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e7225-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7225-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e7225-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e7225-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7225-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e7225-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e7225-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e7225-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7225-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e7225-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e7225-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7225-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e7225-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7225-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span><span class="sxs-lookup"><span data-stu-id="e7225-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="e7225-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e7225-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="e7225-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e7225-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="e7225-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7225-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

1. <span data-ttu-id="e7225-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e7225-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="e7225-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="e7225-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

1. <span data-ttu-id="e7225-158">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="e7225-158">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/opsgenie-tutorial/tutorial_opsgenie_certificate.png)

1. <span data-ttu-id="e7225-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e7225-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/opsgenie-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e7225-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e7225-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7225-163">Copy the **SAML Single Sign-On Service URL** from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="e7225-163">Copy the **SAML Single Sign-On Service URL** from the Quick Reference section.</span></span>

    ![Configure Single Sign-On](./media/opsgenie-tutorial/tutorial_opsgenie_configure.png)

1. <span data-ttu-id="e7225-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e7225-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

1. <span data-ttu-id="e7225-166">Click **Settings**, and then click the **Single Sign On** tab.</span><span class="sxs-lookup"><span data-stu-id="e7225-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![OpsGenie Single Sign-On](./media/opsgenie-tutorial/tutorial_opsgenie_06.png)

1. <span data-ttu-id="e7225-168">To enable SSO, select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="e7225-168">To enable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie Settings](./media/opsgenie-tutorial/tutorial_opsgenie_07.png) 

1. <span data-ttu-id="e7225-170">In the **Provider** section, click the **Azure Active Directory** tab.</span><span class="sxs-lookup"><span data-stu-id="e7225-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie Settings](./media/opsgenie-tutorial/tutorial_opsgenie_08.png) 

1. <span data-ttu-id="e7225-172">On the Azure Active Directory dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e7225-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![OpsGenie Settings](./media/opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="e7225-174">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-174">a.</span></span> <span data-ttu-id="e7225-175">In the **SAML 2.0 Endpoint** textbox, paste **Single Sign On Service URL**value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e7225-175">In the **SAML 2.0 Endpoint** textbox, paste **Single Sign On Service URL**value which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="e7225-176">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-176">b.</span></span> <span data-ttu-id="e7225-177">In the **Metadata Url:** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e7225-177">In the **Metadata Url:** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="e7225-178">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-178">c.</span></span> <span data-ttu-id="e7225-179">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="e7225-179">Click **Save Changes**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7225-180">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e7225-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7225-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7225-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="e7225-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e7225-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7225-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e7225-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/opsgenie-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e7225-186">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e7225-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/opsgenie-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="e7225-188">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e7225-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/opsgenie-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e7225-190">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e7225-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7225-192">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-192">a.</span></span> <span data-ttu-id="e7225-193">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7225-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7225-194">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-194">b.</span></span> <span data-ttu-id="e7225-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7225-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7225-196">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-196">c.</span></span> <span data-ttu-id="e7225-197">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7225-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7225-198">d.</span><span class="sxs-lookup"><span data-stu-id="e7225-198">d.</span></span> <span data-ttu-id="e7225-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e7225-199">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="e7225-200">Creating a OpsGenie test user</span><span class="sxs-lookup"><span data-stu-id="e7225-200">Creating a OpsGenie test user</span></span>

<span data-ttu-id="e7225-201">The objective of this section is to create a user called Britta Simon in OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="e7225-201">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="e7225-202">In a web browser window, log into your OpsGenie tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e7225-202">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

1. <span data-ttu-id="e7225-203">Navigate to Users list by clicking **User** in left panel.</span><span class="sxs-lookup"><span data-stu-id="e7225-203">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie Settings](./media/opsgenie-tutorial/tutorial_opsgenie_10.png) 

1. <span data-ttu-id="e7225-205">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e7225-205">Click **Add User**.</span></span>

1. <span data-ttu-id="e7225-206">On the **Add User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e7225-206">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![OpsGenie Settings](./media/opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="e7225-208">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-208">a.</span></span> <span data-ttu-id="e7225-209">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e7225-209">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="e7225-210">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-210">b.</span></span> <span data-ttu-id="e7225-211">In the **Full Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e7225-211">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="e7225-212">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-212">c.</span></span> <span data-ttu-id="e7225-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e7225-213">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="e7225-214">Britta gets an email with instructions for setting up her profile.</span><span class="sxs-lookup"><span data-stu-id="e7225-214">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7225-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e7225-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7225-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="e7225-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Assign User][200] 

<span data-ttu-id="e7225-218">**To assign Britta Simon to OpsGenie, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e7225-218">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="e7225-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e7225-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e7225-221">In the applications list, select **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="e7225-221">In the applications list, select **OpsGenie**.</span></span>

    ![Configure Single Sign-On](./media/opsgenie-tutorial/tutorial_opsgenie_app.png) 

1. <span data-ttu-id="e7225-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e7225-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="e7225-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e7225-225">Click **Add** button.</span></span> <span data-ttu-id="e7225-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e7225-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="e7225-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e7225-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e7225-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e7225-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e7225-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e7225-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7225-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e7225-231">Testing single sign-on</span></span>

<span data-ttu-id="e7225-232">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e7225-232">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e7225-233">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span><span class="sxs-lookup"><span data-stu-id="e7225-233">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7225-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e7225-234">Additional resources</span></span>

* [<span data-ttu-id="e7225-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7225-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e7225-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7225-236">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/opsgenie-tutorial/tutorial_general_203.png

