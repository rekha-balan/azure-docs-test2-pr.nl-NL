---
title: 'Tutorial: Azure Active Directory integration with Palo Alto Networks - Captive Portal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Palo Alto Networks - Captive Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 67a0b476-2305-4157-8658-2ec3625850d5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: jeedes
ms.openlocfilehash: fa47eaea590ecb84386a6e0ce4eff0a6933be554
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866428"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---captive-portal"></a><span data-ttu-id="e329a-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - Captive Portal</span><span class="sxs-lookup"><span data-stu-id="e329a-103">Tutorial: Azure Active Directory integration with Palo Alto Networks - Captive Portal</span></span>

<span data-ttu-id="e329a-104">In this tutorial, you learn how to integrate Palo Alto Networks - Captive Portal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e329a-104">In this tutorial, you learn how to integrate Palo Alto Networks - Captive Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e329a-105">Integrating Palo Alto Networks - Captive Portal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e329a-105">Integrating Palo Alto Networks - Captive Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e329a-106">You can control in Azure AD who has access to Palo Alto Networks - Captive Portal.</span><span class="sxs-lookup"><span data-stu-id="e329a-106">You can control in Azure AD who has access to Palo Alto Networks - Captive Portal.</span></span>
- <span data-ttu-id="e329a-107">You can enable your users to automatically get signed-on to Palo Alto Networks - Captive Portal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e329a-107">You can enable your users to automatically get signed-on to Palo Alto Networks - Captive Portal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e329a-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e329a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e329a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e329a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e329a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e329a-110">Prerequisites</span></span>

<span data-ttu-id="e329a-111">To configure Azure AD integration with Palo Alto Networks - Captive Portal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e329a-111">To configure Azure AD integration with Palo Alto Networks - Captive Portal, you need the following items:</span></span>

- <span data-ttu-id="e329a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e329a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e329a-113">A Palo Alto Networks - Captive Portal single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e329a-113">A Palo Alto Networks - Captive Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e329a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e329a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e329a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e329a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e329a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e329a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e329a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e329a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e329a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e329a-118">Scenario description</span></span>
<span data-ttu-id="e329a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e329a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e329a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e329a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e329a-121">Adding Palo Alto Networks - Captive Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="e329a-121">Adding Palo Alto Networks - Captive Portal from the gallery</span></span>
1. <span data-ttu-id="e329a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e329a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-palo-alto-networks---captive-portal-from-the-gallery"></a><span data-ttu-id="e329a-123">Adding Palo Alto Networks - Captive Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="e329a-123">Adding Palo Alto Networks - Captive Portal from the gallery</span></span>
<span data-ttu-id="e329a-124">To configure the integration of Palo Alto Networks - Captive Portal into Azure AD, you need to add Palo Alto Networks - Captive Portal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e329a-124">To configure the integration of Palo Alto Networks - Captive Portal into Azure AD, you need to add Palo Alto Networks - Captive Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e329a-125">**To add Palo Alto Networks - Captive Portal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e329a-125">**To add Palo Alto Networks - Captive Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e329a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e329a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e329a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e329a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e329a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e329a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e329a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e329a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e329a-133">In the search box, type **Palo Alto Networks - Captive Portal**, select **Palo Alto Networks - Captive Portal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e329a-133">In the search box, type **Palo Alto Networks - Captive Portal**, select **Palo Alto Networks - Captive Portal** from result panel then click **Add** button to add the application.</span></span>

    ![Palo Alto Networks - Captive Portal in the results list](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltocaptiveportal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e329a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e329a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e329a-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Captive Portal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e329a-136">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Captive Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e329a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - Captive Portal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e329a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Palo Alto Networks - Captive Portal is to a user in Azure AD.</span></span> <span data-ttu-id="e329a-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - Captive Portal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e329a-138">In other words, a link relationship between an Azure AD user and the related user in Palo Alto Networks - Captive Portal needs to be established.</span></span>

<span data-ttu-id="e329a-139">In Palo Alto Networks - Captive Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e329a-139">In Palo Alto Networks - Captive Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e329a-140">To configure and test Azure AD single sign-on with Palo Alto Networks - Captive Portal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e329a-140">To configure and test Azure AD single sign-on with Palo Alto Networks - Captive Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e329a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e329a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e329a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e329a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e329a-143">**[Create a Palo Alto Networks - Captive Portal test user](#create-a-palo-alto-networks---captive-portal-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - Captive Portal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e329a-143">**[Create a Palo Alto Networks - Captive Portal test user](#create-a-palo-alto-networks---captive-portal-test-user)** - to have a counterpart of Britta Simon in Palo Alto Networks - Captive Portal that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e329a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e329a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e329a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e329a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e329a-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e329a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e329a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Captive Portal application.</span><span class="sxs-lookup"><span data-stu-id="e329a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Captive Portal application.</span></span>

<span data-ttu-id="e329a-148">**To configure Azure AD single sign-on with Palo Alto Networks - Captive Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e329a-148">**To configure Azure AD single sign-on with Palo Alto Networks - Captive Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e329a-149">In the Azure portal, on the **Palo Alto Networks - Captive Portal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e329a-149">In the Azure portal, on the **Palo Alto Networks - Captive Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e329a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e329a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltocaptiveportal_samlbase.png)

1. <span data-ttu-id="e329a-153">On the **Palo Alto Networks - Captive Portal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e329a-153">On the **Palo Alto Networks - Captive Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Palo Alto Networks - Captive Portal Domain and URLs single sign-on information](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltocaptiveportal_url.png)

    <span data-ttu-id="e329a-155">a.</span><span class="sxs-lookup"><span data-stu-id="e329a-155">a.</span></span> <span data-ttu-id="e329a-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<Customer Firewall Hostname>/SAML20/SP`</span><span class="sxs-lookup"><span data-stu-id="e329a-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<Customer Firewall Hostname>/SAML20/SP`</span></span>

    <span data-ttu-id="e329a-157">b.</span><span class="sxs-lookup"><span data-stu-id="e329a-157">b.</span></span> <span data-ttu-id="e329a-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer Firewall Hostname>/SAML20/SP/ACS`</span><span class="sxs-lookup"><span data-stu-id="e329a-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer Firewall Hostname>/SAML20/SP/ACS`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e329a-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e329a-159">These values are not real.</span></span> <span data-ttu-id="e329a-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e329a-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e329a-161">Contact [Palo Alto Networks - Captive Portal support team](https://support.paloaltonetworks.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e329a-161">Contact [Palo Alto Networks - Captive Portal support team](https://support.paloaltonetworks.com/support) to get these values.</span></span>

1. <span data-ttu-id="e329a-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e329a-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltocaptiveportal_certificate.png) 

1. <span data-ttu-id="e329a-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e329a-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e329a-166">Open the Palo Alto site as an administrator in another browser window.</span><span class="sxs-lookup"><span data-stu-id="e329a-166">Open the Palo Alto site as an administrator in another browser window.</span></span>

1. <span data-ttu-id="e329a-167">Click on **Device**.</span><span class="sxs-lookup"><span data-stu-id="e329a-167">Click on **Device**.</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin1.png)

1. <span data-ttu-id="e329a-169">Select **SAML Identity Provider** from the left navigation bar and click "Import" to import the metadata file.</span><span class="sxs-lookup"><span data-stu-id="e329a-169">Select **SAML Identity Provider** from the left navigation bar and click "Import" to import the metadata file.</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin2.png)

1. <span data-ttu-id="e329a-171">Perform following actions on the Import window</span><span class="sxs-lookup"><span data-stu-id="e329a-171">Perform following actions on the Import window</span></span>

    ![Configure Palo Alto Single Sign-on](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin3.png)

    <span data-ttu-id="e329a-173">a.</span><span class="sxs-lookup"><span data-stu-id="e329a-173">a.</span></span> <span data-ttu-id="e329a-174">In the **Profile Name** textbox, provide a name e.g Azure AD Admin UI.</span><span class="sxs-lookup"><span data-stu-id="e329a-174">In the **Profile Name** textbox, provide a name e.g Azure AD Admin UI.</span></span>
    
    <span data-ttu-id="e329a-175">b.</span><span class="sxs-lookup"><span data-stu-id="e329a-175">b.</span></span> <span data-ttu-id="e329a-176">In **Identity Provider Metadata**, click **Browse** and select the metadata.xml file which you have downloaded from Azure portal</span><span class="sxs-lookup"><span data-stu-id="e329a-176">In **Identity Provider Metadata**, click **Browse** and select the metadata.xml file which you have downloaded from Azure portal</span></span>
    
    <span data-ttu-id="e329a-177">c.</span><span class="sxs-lookup"><span data-stu-id="e329a-177">c.</span></span> <span data-ttu-id="e329a-178">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="e329a-178">Click **OK**</span></span>

> [!TIP]
> <span data-ttu-id="e329a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e329a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e329a-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e329a-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e329a-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e329a-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e329a-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e329a-182">Create an Azure AD test user</span></span>

<span data-ttu-id="e329a-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e329a-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e329a-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e329a-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e329a-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e329a-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/paloaltonetworks-captiveportal-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e329a-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e329a-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/paloaltonetworks-captiveportal-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e329a-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e329a-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/paloaltonetworks-captiveportal-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e329a-192">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e329a-192">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/paloaltonetworks-captiveportal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e329a-194">a.</span><span class="sxs-lookup"><span data-stu-id="e329a-194">a.</span></span> <span data-ttu-id="e329a-195">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e329a-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e329a-196">b.</span><span class="sxs-lookup"><span data-stu-id="e329a-196">b.</span></span> <span data-ttu-id="e329a-197">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e329a-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e329a-198">c.</span><span class="sxs-lookup"><span data-stu-id="e329a-198">c.</span></span> <span data-ttu-id="e329a-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e329a-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e329a-200">d.</span><span class="sxs-lookup"><span data-stu-id="e329a-200">d.</span></span> <span data-ttu-id="e329a-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e329a-201">Click **Create**.</span></span>
  
### <a name="create-a-palo-alto-networks---captive-portal-test-user"></a><span data-ttu-id="e329a-202">Create a Palo Alto Networks - Captive Portal test user</span><span class="sxs-lookup"><span data-stu-id="e329a-202">Create a Palo Alto Networks - Captive Portal test user</span></span>

<span data-ttu-id="e329a-203">The objective of this section is to create a user called Britta Simon in Palo Alto Networks - Captive Portal.</span><span class="sxs-lookup"><span data-stu-id="e329a-203">The objective of this section is to create a user called Britta Simon in Palo Alto Networks - Captive Portal.</span></span> <span data-ttu-id="e329a-204">Palo Alto Networks - Captive Portal supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e329a-204">Palo Alto Networks - Captive Portal supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e329a-205">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e329a-205">There is no action item for you in this section.</span></span> <span data-ttu-id="e329a-206">A new user is created during an attempt to access Palo Alto Networks - Captive Portal if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e329a-206">A new user is created during an attempt to access Palo Alto Networks - Captive Portal if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="e329a-207">If you need to create a user manually, you need to contact the [Palo Alto Networks - Captive Portal support team](https://support.paloaltonetworks.com/support).</span><span class="sxs-lookup"><span data-stu-id="e329a-207">If you need to create a user manually, you need to contact the [Palo Alto Networks - Captive Portal support team](https://support.paloaltonetworks.com/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e329a-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e329a-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="e329a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Captive Portal.</span><span class="sxs-lookup"><span data-stu-id="e329a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Captive Portal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e329a-211">**To assign Britta Simon to Palo Alto Networks - Captive Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e329a-211">**To assign Britta Simon to Palo Alto Networks - Captive Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e329a-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e329a-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e329a-214">In the applications list, select **Palo Alto Networks - Captive Portal**.</span><span class="sxs-lookup"><span data-stu-id="e329a-214">In the applications list, select **Palo Alto Networks - Captive Portal**.</span></span>

    ![The Palo Alto Networks - Captive Portal link in the Applications list](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltocaptiveportal_app.png)  

1. <span data-ttu-id="e329a-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e329a-216">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e329a-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e329a-218">Click **Add** button.</span></span> <span data-ttu-id="e329a-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e329a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e329a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e329a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e329a-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e329a-222">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e329a-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e329a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e329a-224">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e329a-224">Test single sign-on</span></span>

<span data-ttu-id="e329a-225">Captive Portal is configured behind the firewall on Windows VM.</span><span class="sxs-lookup"><span data-stu-id="e329a-225">Captive Portal is configured behind the firewall on Windows VM.</span></span>  <span data-ttu-id="e329a-226">To test single sign-on on Captive Portal, login on the Windows VM using RDP.</span><span class="sxs-lookup"><span data-stu-id="e329a-226">To test single sign-on on Captive Portal, login on the Windows VM using RDP.</span></span> <span data-ttu-id="e329a-227">From within the RDP session, open a browser to any web site, it should automatically open the SSO url and prompt for authentication.</span><span class="sxs-lookup"><span data-stu-id="e329a-227">From within the RDP session, open a browser to any web site, it should automatically open the SSO url and prompt for authentication.</span></span> <span data-ttu-id="e329a-228">Once Authenticaiton is complete, you should be able to navgiate to web sites.</span><span class="sxs-lookup"><span data-stu-id="e329a-228">Once Authenticaiton is complete, you should be able to navgiate to web sites.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e329a-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e329a-229">Additional resources</span></span>

* [<span data-ttu-id="e329a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e329a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e329a-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e329a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_01.png
[2]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_02.png
[3]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_03.png
[4]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_04.png

[100]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_100.png

[200]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_200.png
[201]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_201.png
[202]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_202.png
[203]: ./media/paloaltonetworks-captiveportal-tutorial/tutorial_general_203.png

