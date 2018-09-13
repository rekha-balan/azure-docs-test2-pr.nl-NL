---
title: 'Tutorial: Azure Active Directory integration with RFPIO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 04ba94e3263af03279b74b4832b8291ad6414274
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855700"
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="d5799-103">Tutorial: Azure Active Directory integration with RFPIO</span><span class="sxs-lookup"><span data-stu-id="d5799-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="d5799-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5799-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5799-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d5799-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d5799-106">You can control who in Azure AD who has access to RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d5799-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="d5799-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d5799-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d5799-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d5799-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="d5799-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d5799-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5799-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d5799-110">Prerequisites</span></span>

<span data-ttu-id="d5799-111">To configure Azure AD integration with RFPIO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d5799-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="d5799-112">An Azure AD subscription.</span><span class="sxs-lookup"><span data-stu-id="d5799-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="d5799-113">A RFPIO single sign-on-enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="d5799-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d5799-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d5799-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="d5799-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d5799-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d5799-116">Do not use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="d5799-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="d5799-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5799-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5799-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d5799-118">Scenario description</span></span>
<span data-ttu-id="d5799-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d5799-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5799-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d5799-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5799-121">Adding RFPIO from the gallery.</span><span class="sxs-lookup"><span data-stu-id="d5799-121">Adding RFPIO from the gallery.</span></span>
1. <span data-ttu-id="d5799-122">Configuring and testing Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5799-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="d5799-123">Add RFPIO from the gallery</span><span class="sxs-lookup"><span data-stu-id="d5799-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="d5799-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d5799-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="d5799-125">To add RFPIO from the gallery</span><span class="sxs-lookup"><span data-stu-id="d5799-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="d5799-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d5799-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d5799-128">Select **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d5799-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d5799-130">To add a new application, select the **New application** button on the top of dialog box.</span><span class="sxs-lookup"><span data-stu-id="d5799-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d5799-132">In the search box, type **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="d5799-132">In the search box, type **RFPIO**.</span></span>

    ![Creating an Azure AD test user](./media/rfpio-tutorial/tutorial_rfpio_search.png)

1. <span data-ttu-id="d5799-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d5799-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d5799-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d5799-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d5799-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d5799-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5799-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5799-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="d5799-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d5799-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="d5799-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d5799-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d5799-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d5799-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d5799-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d5799-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d5799-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5799-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d5799-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d5799-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d5799-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5799-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d5799-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d5799-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d5799-147">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d5799-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d5799-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span><span class="sxs-lookup"><span data-stu-id="d5799-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="d5799-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d5799-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="d5799-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d5799-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d5799-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5799-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_samlbase.png)

1. <span data-ttu-id="d5799-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d5799-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="d5799-156">a.</span><span class="sxs-lookup"><span data-stu-id="d5799-156">a.</span></span> <span data-ttu-id="d5799-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d5799-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="d5799-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5799-159">b.</span></span> <span data-ttu-id="d5799-160">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="d5799-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d5799-161">c.</span><span class="sxs-lookup"><span data-stu-id="d5799-161">c.</span></span> <span data-ttu-id="d5799-162">In the **Relay State** textbox enter a string value.</span><span class="sxs-lookup"><span data-stu-id="d5799-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="d5799-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="d5799-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

1. <span data-ttu-id="d5799-164">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="d5799-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d5799-165">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d5799-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="d5799-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d5799-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

1. <span data-ttu-id="d5799-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d5799-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_certificate.png) 

1. <span data-ttu-id="d5799-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d5799-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d5799-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d5799-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

1. <span data-ttu-id="d5799-173">Click on the bottom left corner dropdown.</span><span class="sxs-lookup"><span data-stu-id="d5799-173">Click on the bottom left corner dropdown.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app1.png)

1. <span data-ttu-id="d5799-175">Click on the **Organization Settings**.</span><span class="sxs-lookup"><span data-stu-id="d5799-175">Click on the **Organization Settings**.</span></span> 

    ![Configure Single Sign-On](./media/rfpio-tutorial/app2.png)

1. <span data-ttu-id="d5799-177">Click on the **FEATURES & INTEGRATION**.</span><span class="sxs-lookup"><span data-stu-id="d5799-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app4.png)

1. <span data-ttu-id="d5799-179">In the **SAML SSO Configuration** Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="d5799-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app3.png)

1. <span data-ttu-id="d5799-181">In this Section perform following actions:</span><span class="sxs-lookup"><span data-stu-id="d5799-181">In this Section perform following actions:</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app5.png)
    
    <span data-ttu-id="d5799-183">a.</span><span class="sxs-lookup"><span data-stu-id="d5799-183">a.</span></span> <span data-ttu-id="d5799-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span><span class="sxs-lookup"><span data-stu-id="d5799-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="d5799-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span><span class="sxs-lookup"><span data-stu-id="d5799-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="d5799-186">b.</span><span class="sxs-lookup"><span data-stu-id="d5799-186">b.</span></span> <span data-ttu-id="d5799-187">Click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="d5799-187">Click **Validate**.</span></span>

    <span data-ttu-id="d5799-188">c.</span><span class="sxs-lookup"><span data-stu-id="d5799-188">c.</span></span> <span data-ttu-id="d5799-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span><span class="sxs-lookup"><span data-stu-id="d5799-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="d5799-190">d.</span><span class="sxs-lookup"><span data-stu-id="d5799-190">d.</span></span> <span data-ttu-id="d5799-191">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d5799-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="d5799-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d5799-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d5799-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d5799-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d5799-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5799-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d5799-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d5799-195">Create an Azure AD test user</span></span>
<span data-ttu-id="d5799-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5799-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d5799-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d5799-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d5799-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d5799-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d5799-201">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d5799-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d5799-203">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d5799-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d5799-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d5799-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5799-207">a.</span><span class="sxs-lookup"><span data-stu-id="d5799-207">a.</span></span> <span data-ttu-id="d5799-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5799-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5799-209">b.</span><span class="sxs-lookup"><span data-stu-id="d5799-209">b.</span></span> <span data-ttu-id="d5799-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5799-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5799-211">c.</span><span class="sxs-lookup"><span data-stu-id="d5799-211">c.</span></span> <span data-ttu-id="d5799-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d5799-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d5799-213">d.</span><span class="sxs-lookup"><span data-stu-id="d5799-213">d.</span></span> <span data-ttu-id="d5799-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d5799-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="d5799-215">Create a RFPIO test user</span><span class="sxs-lookup"><span data-stu-id="d5799-215">Create a RFPIO test user</span></span>

<span data-ttu-id="d5799-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d5799-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="d5799-217">In the case of RFPIO, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="d5799-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="d5799-218">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d5799-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d5799-219">Log in to your RFPIO company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d5799-219">Log in to your RFPIO company site as an administrator.</span></span>

1. <span data-ttu-id="d5799-220">Click on the bottom left corner dropdown.</span><span class="sxs-lookup"><span data-stu-id="d5799-220">Click on the bottom left corner dropdown.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app1.png)

1. <span data-ttu-id="d5799-222">Click on the **Organization Settings**.</span><span class="sxs-lookup"><span data-stu-id="d5799-222">Click on the **Organization Settings**.</span></span> 

    ![Configure Single Sign-On](./media/rfpio-tutorial/app2.png)

1. <span data-ttu-id="d5799-224">Click **TEAM MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="d5799-224">Click **TEAM MEMBERS**.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app6.png)

1. <span data-ttu-id="d5799-226">Click on **ADD MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="d5799-226">Click on **ADD MEMBERS**.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app7.png)

1. <span data-ttu-id="d5799-228">In the **Add New Members** section.</span><span class="sxs-lookup"><span data-stu-id="d5799-228">In the **Add New Members** section.</span></span> <span data-ttu-id="d5799-229">Perform following actions:</span><span class="sxs-lookup"><span data-stu-id="d5799-229">Perform following actions:</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/app8.png)

    <span data-ttu-id="d5799-231">a.</span><span class="sxs-lookup"><span data-stu-id="d5799-231">a.</span></span> <span data-ttu-id="d5799-232">Enter **Email address** in the **Enter one email per line** field.</span><span class="sxs-lookup"><span data-stu-id="d5799-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="d5799-233">b.</span><span class="sxs-lookup"><span data-stu-id="d5799-233">b.</span></span> <span data-ttu-id="d5799-234">Plese select **Role** according your requirements.</span><span class="sxs-lookup"><span data-stu-id="d5799-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="d5799-235">c.</span><span class="sxs-lookup"><span data-stu-id="d5799-235">c.</span></span> <span data-ttu-id="d5799-236">Click **ADD MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="d5799-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="d5799-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="d5799-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d5799-238">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d5799-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="d5799-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d5799-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Assign User][200] 

<span data-ttu-id="d5799-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d5799-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="d5799-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d5799-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d5799-244">In the applications list, select **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="d5799-244">In the applications list, select **RFPIO**.</span></span>

    ![Configure Single Sign-On](./media/rfpio-tutorial/tutorial_rfpio_app.png) 

1. <span data-ttu-id="d5799-246">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d5799-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d5799-248">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d5799-248">Click **Add** button.</span></span> <span data-ttu-id="d5799-249">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d5799-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d5799-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d5799-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d5799-252">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d5799-252">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d5799-253">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d5799-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d5799-254">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d5799-254">Test single sign-on</span></span>

<span data-ttu-id="d5799-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d5799-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="d5799-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span><span class="sxs-lookup"><span data-stu-id="d5799-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="d5799-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5799-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5799-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d5799-258">Additional resources</span></span>

* [<span data-ttu-id="d5799-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5799-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d5799-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d5799-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/rfpio-tutorial/tutorial_general_01.png
[2]: ./media/rfpio-tutorial/tutorial_general_02.png
[3]: ./media/rfpio-tutorial/tutorial_general_03.png
[4]: ./media/rfpio-tutorial/tutorial_general_04.png

[100]: ./media/rfpio-tutorial/tutorial_general_100.png

[200]: ./media/rfpio-tutorial/tutorial_general_200.png
[201]: ./media/rfpio-tutorial/tutorial_general_201.png
[202]: ./media/rfpio-tutorial/tutorial_general_202.png
[203]: ./media/rfpio-tutorial/tutorial_general_203.png

