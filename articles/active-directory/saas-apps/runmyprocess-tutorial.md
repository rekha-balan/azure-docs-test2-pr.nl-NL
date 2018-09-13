---
title: 'Tutorial: Azure Active Directory integration with RunMyProcess | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8cfdbac75036e59cf4acebe07c76ff758b74cdd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969063"
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="388c0-103">Tutorial: Azure Active Directory integration with RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="388c0-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="388c0-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="388c0-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="388c0-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="388c0-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="388c0-106">You can control in Azure AD who has access to RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="388c0-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="388c0-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="388c0-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="388c0-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="388c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="388c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="388c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="388c0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="388c0-110">Prerequisites</span></span>

<span data-ttu-id="388c0-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="388c0-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="388c0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="388c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="388c0-113">A RunMyProcess single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="388c0-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="388c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="388c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="388c0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="388c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="388c0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="388c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="388c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="388c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="388c0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="388c0-118">Scenario description</span></span>
<span data-ttu-id="388c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="388c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="388c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="388c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="388c0-121">Adding RunMyProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="388c0-121">Adding RunMyProcess from the gallery</span></span>
1. <span data-ttu-id="388c0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="388c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="388c0-123">Adding RunMyProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="388c0-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="388c0-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="388c0-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="388c0-125">**To add RunMyProcess from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="388c0-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="388c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="388c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="388c0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="388c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="388c0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="388c0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="388c0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="388c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="388c0-133">In the search box, type **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="388c0-133">In the search box, type **RunMyProcess**.</span></span>

    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/tutorial_runmyprocess_search.png)

1. <span data-ttu-id="388c0-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="388c0-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="388c0-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="388c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="388c0-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="388c0-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="388c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="388c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="388c0-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span><span class="sxs-lookup"><span data-stu-id="388c0-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="388c0-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="388c0-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="388c0-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="388c0-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="388c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="388c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="388c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="388c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="388c0-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="388c0-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="388c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="388c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="388c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="388c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="388c0-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="388c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="388c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span><span class="sxs-lookup"><span data-stu-id="388c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="388c0-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="388c0-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="388c0-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="388c0-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="388c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="388c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

1. <span data-ttu-id="388c0-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="388c0-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="388c0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="388c0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="388c0-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="388c0-158">The value is not real.</span></span> <span data-ttu-id="388c0-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="388c0-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="388c0-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="388c0-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

1. <span data-ttu-id="388c0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="388c0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

1. <span data-ttu-id="388c0-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="388c0-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="388c0-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="388c0-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="388c0-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="388c0-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

1. <span data-ttu-id="388c0-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="388c0-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

1. <span data-ttu-id="388c0-169">In left navigation panel, click **Account** and select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="388c0-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configure Single Sign-On On App Side](./media/runmyprocess-tutorial/tutorial_runmyprocess_001.png)

1. <span data-ttu-id="388c0-171">Go to **Authentication method** section and perform below steps:</span><span class="sxs-lookup"><span data-stu-id="388c0-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Configure Single Sign-On On App Side](./media/runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="388c0-173">a.</span><span class="sxs-lookup"><span data-stu-id="388c0-173">a.</span></span> <span data-ttu-id="388c0-174">As **Method**, select **SSO with Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="388c0-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="388c0-175">b.</span><span class="sxs-lookup"><span data-stu-id="388c0-175">b.</span></span> <span data-ttu-id="388c0-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="388c0-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="388c0-177">c.</span><span class="sxs-lookup"><span data-stu-id="388c0-177">c.</span></span> <span data-ttu-id="388c0-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="388c0-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="388c0-179">d.</span><span class="sxs-lookup"><span data-stu-id="388c0-179">d.</span></span> <span data-ttu-id="388c0-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="388c0-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="388c0-181">e.</span><span class="sxs-lookup"><span data-stu-id="388c0-181">e.</span></span> <span data-ttu-id="388c0-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="388c0-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="388c0-183">f.</span><span class="sxs-lookup"><span data-stu-id="388c0-183">f.</span></span> <span data-ttu-id="388c0-184">Click **Save** icon.</span><span class="sxs-lookup"><span data-stu-id="388c0-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="388c0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="388c0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="388c0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="388c0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="388c0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="388c0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="388c0-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="388c0-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="388c0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="388c0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="388c0-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="388c0-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="388c0-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="388c0-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="388c0-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="388c0-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="388c0-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="388c0-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="388c0-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="388c0-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="388c0-200">a.</span><span class="sxs-lookup"><span data-stu-id="388c0-200">a.</span></span> <span data-ttu-id="388c0-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="388c0-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="388c0-202">b.</span><span class="sxs-lookup"><span data-stu-id="388c0-202">b.</span></span> <span data-ttu-id="388c0-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="388c0-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="388c0-204">c.</span><span class="sxs-lookup"><span data-stu-id="388c0-204">c.</span></span> <span data-ttu-id="388c0-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="388c0-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="388c0-206">d.</span><span class="sxs-lookup"><span data-stu-id="388c0-206">d.</span></span> <span data-ttu-id="388c0-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="388c0-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="388c0-208">Creating a RunMyProcess test user</span><span class="sxs-lookup"><span data-stu-id="388c0-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="388c0-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="388c0-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="388c0-210">In the case of RunMyProcess, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="388c0-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="388c0-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="388c0-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="388c0-212">Log in to your RunMyProcess company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="388c0-212">Log in to your RunMyProcess company site as an administrator.</span></span>

1. <span data-ttu-id="388c0-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span><span class="sxs-lookup"><span data-stu-id="388c0-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="388c0-214">![New User](./media/runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span><span class="sxs-lookup"><span data-stu-id="388c0-214">![New User](./media/runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

1. <span data-ttu-id="388c0-215">In the **User Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="388c0-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="388c0-216">![Profile](./media/runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span><span class="sxs-lookup"><span data-stu-id="388c0-216">![Profile](./media/runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="388c0-217">a.</span><span class="sxs-lookup"><span data-stu-id="388c0-217">a.</span></span> <span data-ttu-id="388c0-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="388c0-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="388c0-219">b.</span><span class="sxs-lookup"><span data-stu-id="388c0-219">b.</span></span> <span data-ttu-id="388c0-220">Select an **IDE language**, **Language**, and **Profile**.</span><span class="sxs-lookup"><span data-stu-id="388c0-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="388c0-221">c.</span><span class="sxs-lookup"><span data-stu-id="388c0-221">c.</span></span> <span data-ttu-id="388c0-222">Select **Send account creation e-mail to me**.</span><span class="sxs-lookup"><span data-stu-id="388c0-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="388c0-223">d.</span><span class="sxs-lookup"><span data-stu-id="388c0-223">d.</span></span> <span data-ttu-id="388c0-224">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="388c0-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="388c0-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="388c0-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="388c0-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="388c0-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="388c0-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="388c0-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Assign User][200] 

<span data-ttu-id="388c0-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="388c0-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="388c0-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="388c0-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="388c0-232">In the applications list, select **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="388c0-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Configure Single Sign-On](./media/runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

1. <span data-ttu-id="388c0-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="388c0-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="388c0-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="388c0-236">Click **Add** button.</span></span> <span data-ttu-id="388c0-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="388c0-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="388c0-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="388c0-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="388c0-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="388c0-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="388c0-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="388c0-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="388c0-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="388c0-242">Testing single sign-on</span></span>

<span data-ttu-id="388c0-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="388c0-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="388c0-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span><span class="sxs-lookup"><span data-stu-id="388c0-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="388c0-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="388c0-245">Additional resources</span></span>

* [<span data-ttu-id="388c0-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="388c0-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="388c0-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="388c0-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/runmyprocess-tutorial/tutorial_general_203.png
