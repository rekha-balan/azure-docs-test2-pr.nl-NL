---
title: 'Tutorial: Azure Active Directory integration with Sugar CRM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sugar CRM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1acaf5e530f5d5563901d8d498901ecc1bffecdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864640"
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="46297-103">Tutorial: Azure Active Directory integration with Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="46297-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="46297-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46297-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46297-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="46297-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46297-106">You can control in Azure AD who has access to Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="46297-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="46297-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="46297-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46297-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="46297-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="46297-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="46297-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46297-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="46297-110">Prerequisites</span></span>

<span data-ttu-id="46297-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="46297-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="46297-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="46297-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46297-113">A Sugar CRM single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="46297-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46297-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="46297-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46297-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="46297-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46297-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="46297-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46297-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46297-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46297-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="46297-118">Scenario description</span></span>
<span data-ttu-id="46297-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="46297-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46297-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="46297-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46297-121">Adding Sugar CRM from the gallery</span><span class="sxs-lookup"><span data-stu-id="46297-121">Adding Sugar CRM from the gallery</span></span>
1. <span data-ttu-id="46297-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46297-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="46297-123">Adding Sugar CRM from the gallery</span><span class="sxs-lookup"><span data-stu-id="46297-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="46297-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="46297-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46297-125">**To add Sugar CRM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46297-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46297-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46297-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="46297-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="46297-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46297-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46297-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="46297-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="46297-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="46297-133">In the search box, type **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="46297-133">In the search box, type **Sugar CRM**.</span></span>

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/tutorial_sugarcrm_search.png)

1. <span data-ttu-id="46297-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="46297-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46297-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46297-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46297-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="46297-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46297-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46297-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="46297-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="46297-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="46297-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="46297-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="46297-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="46297-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46297-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="46297-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="46297-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46297-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="46297-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="46297-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="46297-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46297-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="46297-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="46297-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46297-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46297-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46297-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span><span class="sxs-lookup"><span data-stu-id="46297-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="46297-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46297-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="46297-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="46297-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="46297-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46297-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

1. <span data-ttu-id="46297-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46297-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="46297-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="46297-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="46297-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="46297-158">The value is not real.</span></span> <span data-ttu-id="46297-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="46297-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="46297-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="46297-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
1. <span data-ttu-id="46297-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="46297-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

1. <span data-ttu-id="46297-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="46297-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="46297-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="46297-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="46297-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="46297-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

1. <span data-ttu-id="46297-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="46297-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

1. <span data-ttu-id="46297-169">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="46297-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="46297-170">![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="46297-170">![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")</span></span>

1. <span data-ttu-id="46297-171">In the **Administration** section, click **Password Management**.</span><span class="sxs-lookup"><span data-stu-id="46297-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="46297-172">![Administration](./media/sugarcrm-tutorial/ic795889.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="46297-172">![Administration](./media/sugarcrm-tutorial/ic795889.png "Administration")</span></span>

1. <span data-ttu-id="46297-173">Select **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="46297-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="46297-174">![Administration](./media/sugarcrm-tutorial/ic795890.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="46297-174">![Administration](./media/sugarcrm-tutorial/ic795890.png "Administration")</span></span>

1. <span data-ttu-id="46297-175">In the **SAML Authentication** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46297-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="46297-176">![SAML Authentication](./media/sugarcrm-tutorial/ic795891.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="46297-176">![SAML Authentication](./media/sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="46297-177">a.</span><span class="sxs-lookup"><span data-stu-id="46297-177">a.</span></span> <span data-ttu-id="46297-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="46297-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="46297-179">b.</span><span class="sxs-lookup"><span data-stu-id="46297-179">b.</span></span> <span data-ttu-id="46297-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="46297-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="46297-181">c.</span><span class="sxs-lookup"><span data-stu-id="46297-181">c.</span></span> <span data-ttu-id="46297-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="46297-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="46297-183">d.</span><span class="sxs-lookup"><span data-stu-id="46297-183">d.</span></span> <span data-ttu-id="46297-184">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="46297-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="46297-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="46297-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="46297-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="46297-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="46297-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46297-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46297-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46297-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="46297-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46297-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="46297-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46297-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46297-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46297-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="46297-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="46297-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="46297-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="46297-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="46297-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46297-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46297-200">a.</span><span class="sxs-lookup"><span data-stu-id="46297-200">a.</span></span> <span data-ttu-id="46297-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46297-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46297-202">b.</span><span class="sxs-lookup"><span data-stu-id="46297-202">b.</span></span> <span data-ttu-id="46297-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46297-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46297-204">c.</span><span class="sxs-lookup"><span data-stu-id="46297-204">c.</span></span> <span data-ttu-id="46297-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="46297-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46297-206">d.</span><span class="sxs-lookup"><span data-stu-id="46297-206">d.</span></span> <span data-ttu-id="46297-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="46297-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="46297-208">Creating a Sugar CRM test user</span><span class="sxs-lookup"><span data-stu-id="46297-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="46297-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="46297-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="46297-210">In the case of Sugar CRM, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="46297-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="46297-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46297-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="46297-212">Log in to your **Sugar CRM** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="46297-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

1. <span data-ttu-id="46297-213">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="46297-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="46297-214">![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="46297-214">![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")</span></span>

1. <span data-ttu-id="46297-215">In the **Administration** section, click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="46297-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="46297-216">![Administration](./media/sugarcrm-tutorial/ic795893.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="46297-216">![Administration](./media/sugarcrm-tutorial/ic795893.png "Administration")</span></span>

1. <span data-ttu-id="46297-217">Go to **Users \> Create New User**.</span><span class="sxs-lookup"><span data-stu-id="46297-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="46297-218">![Create New User](./media/sugarcrm-tutorial/ic795894.png "Create New User")</span><span class="sxs-lookup"><span data-stu-id="46297-218">![Create New User](./media/sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

1. <span data-ttu-id="46297-219">On the **User Profile** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46297-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="46297-220">![New User](./media/sugarcrm-tutorial/ic795895.png "New User")</span><span class="sxs-lookup"><span data-stu-id="46297-220">![New User](./media/sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="46297-221">a.</span><span class="sxs-lookup"><span data-stu-id="46297-221">a.</span></span> <span data-ttu-id="46297-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="46297-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
1. <span data-ttu-id="46297-223">As **Status**, select **Active**.</span><span class="sxs-lookup"><span data-stu-id="46297-223">As **Status**, select **Active**.</span></span>

1. <span data-ttu-id="46297-224">On the Password tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46297-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="46297-225">![New User](./media/sugarcrm-tutorial/ic795896.png "New User")</span><span class="sxs-lookup"><span data-stu-id="46297-225">![New User](./media/sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="46297-226">a.</span><span class="sxs-lookup"><span data-stu-id="46297-226">a.</span></span> <span data-ttu-id="46297-227">Type the password into the related textbox.</span><span class="sxs-lookup"><span data-stu-id="46297-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="46297-228">b.</span><span class="sxs-lookup"><span data-stu-id="46297-228">b.</span></span> <span data-ttu-id="46297-229">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="46297-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="46297-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="46297-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="46297-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46297-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="46297-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="46297-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Assign User][200] 

<span data-ttu-id="46297-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46297-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="46297-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46297-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="46297-237">In the applications list, select **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="46297-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

1. <span data-ttu-id="46297-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="46297-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="46297-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="46297-241">Click **Add** button.</span></span> <span data-ttu-id="46297-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46297-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="46297-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="46297-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="46297-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="46297-245">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="46297-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46297-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46297-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="46297-247">Testing single sign-on</span></span>

<span data-ttu-id="46297-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="46297-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="46297-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span><span class="sxs-lookup"><span data-stu-id="46297-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46297-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="46297-250">Additional resources</span></span>

* [<span data-ttu-id="46297-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46297-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="46297-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46297-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/sugarcrm-tutorial/tutorial_general_203.png

