---
title: 'Tutorial: Azure Active Directory integration with TargetProcess | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TargetProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b79fa31aed1a264ba52675857c9a80dc65746173
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967834"
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="166ab-103">Tutorial: Azure Active Directory integration with TargetProcess</span><span class="sxs-lookup"><span data-stu-id="166ab-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="166ab-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="166ab-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="166ab-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="166ab-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="166ab-106">You can control in Azure AD who has access to TargetProcess</span><span class="sxs-lookup"><span data-stu-id="166ab-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="166ab-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="166ab-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="166ab-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="166ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="166ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="166ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="166ab-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="166ab-110">Prerequisites</span></span>

<span data-ttu-id="166ab-111">To configure Azure AD integration with TargetProcess, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="166ab-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="166ab-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="166ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="166ab-113">A TargetProcess single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="166ab-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="166ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="166ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="166ab-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="166ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="166ab-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="166ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="166ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="166ab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="166ab-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="166ab-118">Scenario description</span></span>
<span data-ttu-id="166ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="166ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="166ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="166ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="166ab-121">Add TargetProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="166ab-121">Add TargetProcess from the gallery</span></span>
1. <span data-ttu-id="166ab-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="166ab-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="166ab-123">Add TargetProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="166ab-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="166ab-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="166ab-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="166ab-125">**To add TargetProcess from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="166ab-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="166ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="166ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="166ab-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="166ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="166ab-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="166ab-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="166ab-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="166ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="166ab-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="166ab-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![ADD TargetProcess from gallery](./media/target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="166ab-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="166ab-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="166ab-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="166ab-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="166ab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="166ab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="166ab-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span><span class="sxs-lookup"><span data-stu-id="166ab-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="166ab-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="166ab-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="166ab-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="166ab-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="166ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="166ab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="166ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="166ab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="166ab-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="166ab-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="166ab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="166ab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="166ab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="166ab-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="166ab-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="166ab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="166ab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span><span class="sxs-lookup"><span data-stu-id="166ab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="166ab-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="166ab-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="166ab-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="166ab-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="166ab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="166ab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML-based Sign-on](./media/target-process-tutorial/tutorial_target-process_samlbase.png)

1. <span data-ttu-id="166ab-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="166ab-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![TargetProcess Domain and URLs section](./media/target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="166ab-155">a.</span><span class="sxs-lookup"><span data-stu-id="166ab-155">a.</span></span> <span data-ttu-id="166ab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="166ab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="166ab-157">b.</span><span class="sxs-lookup"><span data-stu-id="166ab-157">b.</span></span> <span data-ttu-id="166ab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="166ab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="166ab-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="166ab-159">These values are not real.</span></span> <span data-ttu-id="166ab-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="166ab-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="166ab-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="166ab-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
1. <span data-ttu-id="166ab-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="166ab-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/target-process-tutorial/tutorial_target-process_certificate.png) 

1. <span data-ttu-id="166ab-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="166ab-164">Click **Save** button.</span></span>

    ![Save button](./media/target-process-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="166ab-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="166ab-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="166ab-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="166ab-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TargetProcess Configuration section](./media/target-process-tutorial/tutorial_target-process_configure.png) 

1. <span data-ttu-id="166ab-169">Sign-on to your TargetProcess application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="166ab-169">Sign-on to your TargetProcess application as an administrator.</span></span>

1. <span data-ttu-id="166ab-170">In the menu on the top, click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="166ab-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Setup](./media/target-process-tutorial/tutorial_target_process_05.png)

1. <span data-ttu-id="166ab-172">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="166ab-172">Click **Settings**.</span></span>
   
    ![Settings](./media/target-process-tutorial/tutorial_target_process_06.png) 

1. <span data-ttu-id="166ab-174">Click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="166ab-174">Click **Single Sign-on**.</span></span>
   
    ![click Single Sign-On](./media/target-process-tutorial/tutorial_target_process_07.png) 

1. <span data-ttu-id="166ab-176">On the Single Sign-on settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="166ab-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="166ab-178">a.</span><span class="sxs-lookup"><span data-stu-id="166ab-178">a.</span></span> <span data-ttu-id="166ab-179">Click **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="166ab-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="166ab-180">b.</span><span class="sxs-lookup"><span data-stu-id="166ab-180">b.</span></span> <span data-ttu-id="166ab-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="166ab-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="166ab-182">c.</span><span class="sxs-lookup"><span data-stu-id="166ab-182">c.</span></span> <span data-ttu-id="166ab-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="166ab-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="166ab-184">d.</span><span class="sxs-lookup"><span data-stu-id="166ab-184">d.</span></span> <span data-ttu-id="166ab-185">click **Enable JIT Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="166ab-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="166ab-186">e.</span><span class="sxs-lookup"><span data-stu-id="166ab-186">e.</span></span> <span data-ttu-id="166ab-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="166ab-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="166ab-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="166ab-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="166ab-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="166ab-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="166ab-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="166ab-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="166ab-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="166ab-191">Create an Azure AD test user</span></span>
<span data-ttu-id="166ab-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="166ab-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="166ab-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="166ab-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="166ab-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="166ab-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/target-process-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="166ab-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="166ab-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![To display the list of users](./media/target-process-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="166ab-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="166ab-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add button](./media/target-process-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="166ab-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="166ab-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![User section](./media/target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="166ab-203">a.</span><span class="sxs-lookup"><span data-stu-id="166ab-203">a.</span></span> <span data-ttu-id="166ab-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="166ab-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="166ab-205">b.</span><span class="sxs-lookup"><span data-stu-id="166ab-205">b.</span></span> <span data-ttu-id="166ab-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="166ab-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="166ab-207">c.</span><span class="sxs-lookup"><span data-stu-id="166ab-207">c.</span></span> <span data-ttu-id="166ab-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="166ab-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="166ab-209">d.</span><span class="sxs-lookup"><span data-stu-id="166ab-209">d.</span></span> <span data-ttu-id="166ab-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="166ab-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="166ab-211">Create a TargetProcess test user</span><span class="sxs-lookup"><span data-stu-id="166ab-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="166ab-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="166ab-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="166ab-213">TargetProcess supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="166ab-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="166ab-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="166ab-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="166ab-215">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="166ab-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="166ab-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="166ab-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="166ab-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="166ab-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Assign User][200] 

<span data-ttu-id="166ab-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="166ab-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="166ab-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="166ab-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="166ab-222">In the applications list, select **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="166ab-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess in app list](./media/target-process-tutorial/tutorial_target-process_app.png) 

1. <span data-ttu-id="166ab-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="166ab-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="166ab-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="166ab-226">Click **Add** button.</span></span> <span data-ttu-id="166ab-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="166ab-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="166ab-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="166ab-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="166ab-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="166ab-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="166ab-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="166ab-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="166ab-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="166ab-232">Test single sign-on</span></span>

<span data-ttu-id="166ab-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="166ab-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="166ab-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span><span class="sxs-lookup"><span data-stu-id="166ab-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="166ab-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="166ab-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="166ab-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="166ab-236">Additional resources</span></span>

* [<span data-ttu-id="166ab-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="166ab-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="166ab-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="166ab-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/target-process-tutorial/tutorial_general_01.png
[2]: ./media/target-process-tutorial/tutorial_general_02.png
[3]: ./media/target-process-tutorial/tutorial_general_03.png
[4]: ./media/target-process-tutorial/tutorial_general_04.png

[100]: ./media/target-process-tutorial/tutorial_general_100.png

[200]: ./media/target-process-tutorial/tutorial_general_200.png
[201]: ./media/target-process-tutorial/tutorial_general_201.png
[202]: ./media/target-process-tutorial/tutorial_general_202.png
[203]: ./media/target-process-tutorial/tutorial_general_203.png

