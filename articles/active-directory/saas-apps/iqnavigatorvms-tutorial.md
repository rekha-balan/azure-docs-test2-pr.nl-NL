---
title: 'Tutorial: Azure Active Directory integration with IQNavigator VMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: jeedes
ms.openlocfilehash: f568f33de348289334c4b4c346e9525e28cce51c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856747"
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="1fd1a-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="1fd1a-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="1fd1a-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fd1a-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fd1a-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fd1a-106">You can control in Azure AD who has access to IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="1fd1a-106">You can control in Azure AD who has access to IQNavigator VMS</span></span>
- <span data-ttu-id="1fd1a-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1fd1a-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fd1a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fd1a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1fd1a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1fd1a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fd1a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1fd1a-110">Prerequisites</span></span>

<span data-ttu-id="1fd1a-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span></span>

- <span data-ttu-id="1fd1a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1fd1a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fd1a-113">A IQNavigator VMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1fd1a-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fd1a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fd1a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fd1a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fd1a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fd1a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fd1a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1fd1a-118">Scenario description</span></span>
<span data-ttu-id="1fd1a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fd1a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fd1a-121">Adding IQNavigator VMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="1fd1a-121">Adding IQNavigator VMS from the gallery</span></span>
1. <span data-ttu-id="1fd1a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1fd1a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-the-gallery"></a><span data-ttu-id="1fd1a-123">Adding IQNavigator VMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="1fd1a-123">Adding IQNavigator VMS from the gallery</span></span>
<span data-ttu-id="1fd1a-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fd1a-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fd1a-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fd1a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="1fd1a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fd1a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="1fd1a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="1fd1a-133">In the search box, type **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-133">In the search box, type **IQNavigator VMS**.</span></span>

    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

1. <span data-ttu-id="1fd1a-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1fd1a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1fd1a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1fd1a-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fd1a-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fd1a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span></span> <span data-ttu-id="1fd1a-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span></span>

<span data-ttu-id="1fd1a-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fd1a-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fd1a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1fd1a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1fd1a-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1fd1a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1fd1a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1fd1a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1fd1a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1fd1a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="1fd1a-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fd1a-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="1fd1a-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="1fd1a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

1. <span data-ttu-id="1fd1a-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="1fd1a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-157">a.</span></span> <span data-ttu-id="1fd1a-158">In the **Identifier** textbox, type the URL:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="1fd1a-158">In the **Identifier** textbox, type the URL:`iqn.com`</span></span>

    <span data-ttu-id="1fd1a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-159">b.</span></span> <span data-ttu-id="1fd1a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="1fd1a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

1. <span data-ttu-id="1fd1a-161">Check **Show advanced URL settings**, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-161">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="1fd1a-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="1fd1a-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="1fd1a-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-164">These values are not real.</span></span> <span data-ttu-id="1fd1a-165">Update these values with the actual Reply URL and Relay state.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-165">Update these values with the actual Reply URL and Relay state.</span></span> <span data-ttu-id="1fd1a-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span></span>

1. <span data-ttu-id="1fd1a-167">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-167">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_metadataurl.png)

1. <span data-ttu-id="1fd1a-169">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-169">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="1fd1a-170">Customer can map the correct value for the Name Identifier claim.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-170">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="1fd1a-171">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-171">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span></span> <span data-ttu-id="1fd1a-172">But according to your organization settings you should map the correct value for it.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-172">But according to your organization settings you should map the correct value for it.</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

1. <span data-ttu-id="1fd1a-174">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-174">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1fd1a-176">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-176">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1fd1a-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1fd1a-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png)

1. <span data-ttu-id="1fd1a-179">To configure single sign-on on **IQNavigator VMS** side, you need to send the **App Federation Metadata Url**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="1fd1a-179">To configure single sign-on on **IQNavigator VMS** side, you need to send the **App Federation Metadata Url**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="1fd1a-180">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fd1a-181">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1fd1a-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fd1a-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="1fd1a-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fd1a-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fd1a-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="1fd1a-187">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1fd1a-189">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1fd1a-191">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fd1a-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fd1a-193">a.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-193">a.</span></span> <span data-ttu-id="1fd1a-194">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fd1a-195">b.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-195">b.</span></span> <span data-ttu-id="1fd1a-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fd1a-197">c.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-197">c.</span></span> <span data-ttu-id="1fd1a-198">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1fd1a-199">d.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-199">d.</span></span> <span data-ttu-id="1fd1a-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-200">Click **Create**.</span></span>

### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="1fd1a-201">Creating a IQNavigator VMS test user</span><span class="sxs-lookup"><span data-stu-id="1fd1a-201">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="1fd1a-202">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-202">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="1fd1a-203">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-203">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1fd1a-204">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1fd1a-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1fd1a-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span></span>

![Assign User][200]

<span data-ttu-id="1fd1a-207">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fd1a-207">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="1fd1a-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="1fd1a-210">In the applications list, select **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-210">In the applications list, select **IQNavigator VMS**.</span></span>

    ![Configure Single Sign-On](./media/iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png)

1. <span data-ttu-id="1fd1a-212">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="1fd1a-214">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-214">Click **Add** button.</span></span> <span data-ttu-id="1fd1a-215">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="1fd1a-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1fd1a-218">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-218">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1fd1a-219">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1fd1a-220">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="1fd1a-220">Testing single sign-on</span></span>

<span data-ttu-id="1fd1a-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1fd1a-222">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span><span class="sxs-lookup"><span data-stu-id="1fd1a-222">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span></span>
<span data-ttu-id="1fd1a-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1fd1a-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fd1a-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1fd1a-224">Additional resources</span></span>

* [<span data-ttu-id="1fd1a-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fd1a-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1fd1a-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fd1a-226">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/iqnavigatorvms-tutorial/tutorial_general_203.png

