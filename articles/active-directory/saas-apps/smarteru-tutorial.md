---
title: 'Tutorial: Azure Active Directory integration with SmarterU | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SmarterU.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 12c7a2751b980ef7951be9043a62dbb1ec50a63d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857796"
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="bbbcf-103">Tutorial: Azure Active Directory integration with SmarterU</span><span class="sxs-lookup"><span data-stu-id="bbbcf-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="bbbcf-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbbcf-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbbcf-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbbcf-106">You can control in Azure AD who has access to SmarterU</span><span class="sxs-lookup"><span data-stu-id="bbbcf-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="bbbcf-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bbbcf-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbbcf-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bbbcf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbbcf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bbbcf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbbcf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bbbcf-110">Prerequisites</span></span>

<span data-ttu-id="bbbcf-111">To configure Azure AD integration with SmarterU, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="bbbcf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bbbcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbbcf-113">A SmarterU single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bbbcf-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbbcf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbbcf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbbcf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbbcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbbcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbbcf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bbbcf-118">Scenario description</span></span>
<span data-ttu-id="bbbcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbbcf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbbcf-121">Adding SmarterU from the gallery</span><span class="sxs-lookup"><span data-stu-id="bbbcf-121">Adding SmarterU from the gallery</span></span>
1. <span data-ttu-id="bbbcf-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbbcf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="bbbcf-123">Adding SmarterU from the gallery</span><span class="sxs-lookup"><span data-stu-id="bbbcf-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="bbbcf-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbbcf-125">**To add SmarterU from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbbcf-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbbcf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bbbcf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbbcf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bbbcf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bbbcf-133">In the search box, type **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-133">In the search box, type **SmarterU**.</span></span>

    ![Creating an Azure AD test user](./media/smarteru-tutorial/tutorial_smarteru_search.png)

1. <span data-ttu-id="bbbcf-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbbcf-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbbcf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbbcf-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bbbcf-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbbcf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="bbbcf-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="bbbcf-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbbcf-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbbcf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bbbcf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bbbcf-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bbbcf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bbbcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbbcf-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbbcf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbbcf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="bbbcf-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbbcf-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="bbbcf-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bbbcf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/smarteru-tutorial/tutorial_smarteru_samlbase.png)

1. <span data-ttu-id="bbbcf-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Configure Single Sign-On](./media/smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="bbbcf-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="bbbcf-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

1. <span data-ttu-id="bbbcf-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/smarteru-tutorial/tutorial_smarteru_certificate.png) 

1. <span data-ttu-id="bbbcf-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/smarteru-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bbbcf-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

1. <span data-ttu-id="bbbcf-163">In the toolbar on the top, click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    ![Account Settings](./media/smarteru-tutorial/accountsettings.png)

1. <span data-ttu-id="bbbcf-165">On the account configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-165">On the account configuration page, perform the following steps:</span></span>
   
    ![External Authorization](./media/smarteru-tutorial/externalauthorizationconfiguration.png) 
 
      <span data-ttu-id="bbbcf-167">a.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-167">a.</span></span> <span data-ttu-id="bbbcf-168">Select **Enable External Authorization**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="bbbcf-169">b.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-169">b.</span></span> <span data-ttu-id="bbbcf-170">In the **Master Login Control** section, select the **SmarterU** tab.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="bbbcf-171">c.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-171">c.</span></span> <span data-ttu-id="bbbcf-172">In the **User Default Login** section, select the **SmarterU** tab.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="bbbcf-173">d.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-173">d.</span></span> <span data-ttu-id="bbbcf-174">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-174">Select **Enable SAML**.</span></span>
  
      <span data-ttu-id="bbbcf-175">e.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-175">e.</span></span> <span data-ttu-id="bbbcf-176">Copy the content of the downloaded metadata file, and then paste it into the **IdP Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-176">Copy the content of the downloaded metadata file, and then paste it into the **IdP Metadata** textbox.</span></span>
      
      <span data-ttu-id="bbbcf-177">f.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-177">f.</span></span> <span data-ttu-id="bbbcf-178">Select an **Identifier Attribute/Claim**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-178">Select an **Identifier Attribute/Claim**.</span></span>
  
      <span data-ttu-id="bbbcf-179">g.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-179">g.</span></span> <span data-ttu-id="bbbcf-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bbbcf-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bbbcf-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbbcf-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbbcf-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbbcf-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbbcf-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bbbcf-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbbcf-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bbbcf-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbbcf-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbbcf-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/smarteru-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bbbcf-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/smarteru-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bbbcf-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/smarteru-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bbbcf-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbbcf-196">a.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-196">a.</span></span> <span data-ttu-id="bbbcf-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbbcf-198">b.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-198">b.</span></span> <span data-ttu-id="bbbcf-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbbcf-200">c.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-200">c.</span></span> <span data-ttu-id="bbbcf-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbbcf-202">d.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-202">d.</span></span> <span data-ttu-id="bbbcf-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-203">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="bbbcf-204">Creating a SmarterU test user</span><span class="sxs-lookup"><span data-stu-id="bbbcf-204">Creating a SmarterU test user</span></span>

<span data-ttu-id="bbbcf-205">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-205">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="bbbcf-206">When SmarterU, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-206">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="bbbcf-207">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbbcf-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bbbcf-208">Log in to your **SmarterU** tenant.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-208">Log in to your **SmarterU** tenant.</span></span>

1. <span data-ttu-id="bbbcf-209">Go to **Users**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-209">Go to **Users**.</span></span>

1. <span data-ttu-id="bbbcf-210">In the user section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbbcf-210">In the user section, perform the following steps:</span></span>
   
    ![New User](./media/smarteru-tutorial/adduser.png)  

    <span data-ttu-id="bbbcf-212">a.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-212">a.</span></span> <span data-ttu-id="bbbcf-213">Click **+User**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-213">Click **+User**.</span></span>
    
    <span data-ttu-id="bbbcf-214">b.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-214">b.</span></span> <span data-ttu-id="bbbcf-215">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-215">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="bbbcf-216">c.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-216">c.</span></span> <span data-ttu-id="bbbcf-217">Click **Active**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-217">Click **Active**.</span></span> 
    
    <span data-ttu-id="bbbcf-218">d.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-218">d.</span></span> <span data-ttu-id="bbbcf-219">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-219">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="bbbcf-220">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-220">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bbbcf-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bbbcf-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bbbcf-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Assign User][200] 

<span data-ttu-id="bbbcf-224">**To assign Britta Simon to SmarterU, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbbcf-224">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="bbbcf-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bbbcf-227">In the applications list, select **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-227">In the applications list, select **SmarterU**.</span></span>

    ![Configure Single Sign-On](./media/smarteru-tutorial/tutorial_smarteru_app.png) 

1. <span data-ttu-id="bbbcf-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bbbcf-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-231">Click **Add** button.</span></span> <span data-ttu-id="bbbcf-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bbbcf-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bbbcf-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bbbcf-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbbcf-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbbcf-237">Testing single sign-on</span></span>

<span data-ttu-id="bbbcf-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="bbbcf-239">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span><span class="sxs-lookup"><span data-stu-id="bbbcf-239">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="bbbcf-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbbcf-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="bbbcf-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bbbcf-241">Additional resources</span></span>

* [<span data-ttu-id="bbbcf-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbbcf-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bbbcf-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbbcf-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/smarteru-tutorial/tutorial_general_01.png
[2]: ./media/smarteru-tutorial/tutorial_general_02.png
[3]: ./media/smarteru-tutorial/tutorial_general_03.png
[4]: ./media/smarteru-tutorial/tutorial_general_04.png

[100]: ./media/smarteru-tutorial/tutorial_general_100.png

[200]: ./media/smarteru-tutorial/tutorial_general_200.png
[201]: ./media/smarteru-tutorial/tutorial_general_201.png
[202]: ./media/smarteru-tutorial/tutorial_general_202.png
[203]: ./media/smarteru-tutorial/tutorial_general_203.png

