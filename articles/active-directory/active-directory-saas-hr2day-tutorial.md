---
title: 'Tutorial: Azure Active Directory integration with HR2day by Merces | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HR2day by Merces.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 18d5b5981106a17b354ba1bf3a415c1249ff015f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554686"
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="62192-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="62192-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>
<span data-ttu-id="62192-104">The objective of this tutorial is to show you how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62192-104">The objective of this tutorial is to show you how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="62192-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="62192-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="62192-106">You can control in Azure AD who has access to HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="62192-106">You can control in Azure AD who has access to HR2day by Merces</span></span>
* <span data-ttu-id="62192-107">You can enable your users to automatically get signed-on to HR2day by Merces (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="62192-107">You can enable your users to automatically get signed-on to HR2day by Merces (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="62192-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="62192-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="62192-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62192-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62192-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="62192-110">Prerequisites</span></span>
<span data-ttu-id="62192-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="62192-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

* <span data-ttu-id="62192-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="62192-112">An Azure AD subscription</span></span>
* <span data-ttu-id="62192-113">A HR2day by Merces single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="62192-113">A HR2day by Merces single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62192-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="62192-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="62192-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="62192-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="62192-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="62192-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="62192-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62192-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62192-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="62192-118">Scenario Description</span></span>
<span data-ttu-id="62192-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="62192-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="62192-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="62192-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62192-121">Adding HR2day by Merces from the gallery</span><span class="sxs-lookup"><span data-stu-id="62192-121">Adding HR2day by Merces from the gallery</span></span>
2. <span data-ttu-id="62192-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="62192-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="62192-123">Adding HR2day by Merces from the gallery</span><span class="sxs-lookup"><span data-stu-id="62192-123">Adding HR2day by Merces from the gallery</span></span>
<span data-ttu-id="62192-124">To configure the integration of HR2day by Merces into Azure AD, you need to add HR2day by Merces from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="62192-124">To configure the integration of HR2day by Merces into Azure AD, you need to add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62192-125">**To add HR2day by Merces from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62192-125">**To add HR2day by Merces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62192-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62192-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="62192-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="62192-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="62192-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="62192-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="62192-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="62192-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="62192-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="62192-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="62192-135">In the search box, type **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="62192-135">In the search box, type **HR2day by Merces**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_01.png)

7. <span data-ttu-id="62192-137">In the results pane, select **HR2day by Merces**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="62192-137">In the results pane, select **HR2day by Merces**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62192-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="62192-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62192-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="62192-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62192-140">For single sign-on to work, Azure AD needs to know what the counterpart user in HR2day by Merces to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="62192-140">For single sign-on to work, Azure AD needs to know what the counterpart user in HR2day by Merces to an user in Azure AD is.</span></span> <span data-ttu-id="62192-141">In other words, a link relationship between an Azure AD user and the related user in HR2day by Merces needs to be established.</span><span class="sxs-lookup"><span data-stu-id="62192-141">In other words, a link relationship between an Azure AD user and the related user in HR2day by Merces needs to be established.</span></span>  
<span data-ttu-id="62192-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="62192-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HR2day by Merces.</span></span>

<span data-ttu-id="62192-143">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="62192-143">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62192-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="62192-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62192-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62192-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62192-146">**[Creating a HR2day by Merces test user](#creating-a-hr2day-by-merces-test-user)** - to have a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="62192-146">**[Creating a HR2day by Merces test user](#creating-a-hr2day-by-merces-test-user)** - to have a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="62192-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="62192-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62192-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="62192-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62192-149">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="62192-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="62192-150">The objective of this section is to outline how to enable users to authenticate to HR2day by Merces with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="62192-150">The objective of this section is to outline how to enable users to authenticate to HR2day by Merces with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="62192-151">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="62192-151">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="62192-152">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="62192-152">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png) 

<span data-ttu-id="62192-154">Before you can configure the SAML assertion, you need to contact your HR2day support team via [servicedesk@merces.nl](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="62192-154">Before you can configure the SAML assertion, you need to contact your HR2day support team via [servicedesk@merces.nl](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="62192-155">You need this value to complete the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="62192-155">You need this value to complete the steps in the next section.</span></span>

<span data-ttu-id="62192-156">**To configure Azure AD single sign-on with HR2day by Merces, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62192-156">**To configure Azure AD single sign-on with HR2day by Merces, perform the following steps:**</span></span>

1. <span data-ttu-id="62192-157">In the Azure classic portal, on the **HR2day by Merces** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="62192-157">In the Azure classic portal, on the **HR2day by Merces** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_06.png) 

2. <span data-ttu-id="62192-159">To add the required attribute mappings, perform the following steps, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-159">To add the required attribute mappings, perform the following steps, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_07.png) 

    <span data-ttu-id="62192-161">a.</span><span class="sxs-lookup"><span data-stu-id="62192-161">a.</span></span> <span data-ttu-id="62192-162">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="62192-162">Click **add user attribute**.</span></span>

    <span data-ttu-id="62192-163">b.</span><span class="sxs-lookup"><span data-stu-id="62192-163">b.</span></span> <span data-ttu-id="62192-164">In the **Attribute Name** textbox, type **“ATTR_LOGINCLAIM”**.</span><span class="sxs-lookup"><span data-stu-id="62192-164">In the **Attribute Name** textbox, type **“ATTR_LOGINCLAIM”**.</span></span>

    <span data-ttu-id="62192-165">c.</span><span class="sxs-lookup"><span data-stu-id="62192-165">c.</span></span> <span data-ttu-id="62192-166">From the **Attribute Value** list, select **Join()**.</span><span class="sxs-lookup"><span data-stu-id="62192-166">From the **Attribute Value** list, select **Join()**.</span></span> 

    <span data-ttu-id="62192-167">d.</span><span class="sxs-lookup"><span data-stu-id="62192-167">d.</span></span> <span data-ttu-id="62192-168">From the **String1** list, select **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="62192-168">From the **String1** list, select **User.mail**.</span></span> 

    <span data-ttu-id="62192-169">e.</span><span class="sxs-lookup"><span data-stu-id="62192-169">e.</span></span> <span data-ttu-id="62192-170">In the **String2** textbox, type the **unique identifier** provided by your HR2day team.</span><span class="sxs-lookup"><span data-stu-id="62192-170">In the **String2** textbox, type the **unique identifier** provided by your HR2day team.</span></span> 

    <span data-ttu-id="62192-171">f.</span><span class="sxs-lookup"><span data-stu-id="62192-171">f.</span></span> <span data-ttu-id="62192-172">In the **Separator** textbox, type **@**.</span><span class="sxs-lookup"><span data-stu-id="62192-172">In the **Separator** textbox, type **@**.</span></span>

    <span data-ttu-id="62192-173">g.</span><span class="sxs-lookup"><span data-stu-id="62192-173">g.</span></span> <span data-ttu-id="62192-174">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="62192-174">Click **Complete**.</span></span>


1. <span data-ttu-id="62192-175">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="62192-175">Click **Apply Changes**.</span></span>

2. <span data-ttu-id="62192-176">In the menu on the top, click **Quick Start** to open the **Quick Start** dialog.</span><span class="sxs-lookup"><span data-stu-id="62192-176">In the menu on the top, click **Quick Start** to open the **Quick Start** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_08.png) 

3. <span data-ttu-id="62192-178">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="62192-178">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

4. <span data-ttu-id="62192-180">On the **How would you like users to sign on to HR2day by Merces** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-180">On the **How would you like users to sign on to HR2day by Merces** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_03.png) 

5. <span data-ttu-id="62192-182">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-182">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_04.png) 

    <span data-ttu-id="62192-184">a.</span><span class="sxs-lookup"><span data-stu-id="62192-184">a.</span></span> <span data-ttu-id="62192-185">In the Sign On URL textbox, type the URL used by your users to sign-on to your HR2day by Merces application using the following pattern: **“https://\<tenant name\>.force.com/\<instance name\>”**.</span><span class="sxs-lookup"><span data-stu-id="62192-185">In the Sign On URL textbox, type the URL used by your users to sign-on to your HR2day by Merces application using the following pattern: **“https://\<tenant name\>.force.com/\<instance name\>”**.</span></span>

    <span data-ttu-id="62192-186">b.</span><span class="sxs-lookup"><span data-stu-id="62192-186">b.</span></span> <span data-ttu-id="62192-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-187">Click **Next**.</span></span>

1. <span data-ttu-id="62192-188">On the **Configure single sign-on at HR2day by Merces** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-188">On the **Configure single sign-on at HR2day by Merces** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_05.png) 
   
    <span data-ttu-id="62192-190">a.</span><span class="sxs-lookup"><span data-stu-id="62192-190">a.</span></span> <span data-ttu-id="62192-191">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="62192-191">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="62192-192">b.</span><span class="sxs-lookup"><span data-stu-id="62192-192">b.</span></span> <span data-ttu-id="62192-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-193">Click **Next**.</span></span>

2. <span data-ttu-id="62192-194">To get SSO configured for your application, contact your HR2day by Merces support team via [servicedesk@merces.nl](emailTo:servicedesk@merces.nl) and attach the downloaded certificate file to your email.</span><span class="sxs-lookup"><span data-stu-id="62192-194">To get SSO configured for your application, contact your HR2day by Merces support team via [servicedesk@merces.nl](emailTo:servicedesk@merces.nl) and attach the downloaded certificate file to your email.</span></span> <span data-ttu-id="62192-195">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="62192-195">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="62192-196">Please mention to Merces team that this integration need Entity ID to be set with this pattern **https://hr2day.force.com/INSTANCENAME**</span><span class="sxs-lookup"><span data-stu-id="62192-196">Please mention to Merces team that this integration need Entity ID to be set with this pattern **https://hr2day.force.com/INSTANCENAME**</span></span>
    > 
    > 

1. <span data-ttu-id="62192-197">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-197">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
2. <span data-ttu-id="62192-199">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="62192-199">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62192-201">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="62192-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="62192-202">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62192-202">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="62192-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62192-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62192-205">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62192-205">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="62192-207">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="62192-207">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="62192-208">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="62192-208">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62192-210">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="62192-210">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="62192-212">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-212">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="62192-214">a.</span><span class="sxs-lookup"><span data-stu-id="62192-214">a.</span></span> <span data-ttu-id="62192-215">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="62192-215">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="62192-216">b.</span><span class="sxs-lookup"><span data-stu-id="62192-216">b.</span></span> <span data-ttu-id="62192-217">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62192-217">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="62192-218">c.</span><span class="sxs-lookup"><span data-stu-id="62192-218">c.</span></span> <span data-ttu-id="62192-219">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-219">Click **Next**.</span></span>

6. <span data-ttu-id="62192-220">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-220">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="62192-222">a.</span><span class="sxs-lookup"><span data-stu-id="62192-222">a.</span></span> <span data-ttu-id="62192-223">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="62192-223">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="62192-224">b.</span><span class="sxs-lookup"><span data-stu-id="62192-224">b.</span></span> <span data-ttu-id="62192-225">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="62192-225">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="62192-226">c.</span><span class="sxs-lookup"><span data-stu-id="62192-226">c.</span></span> <span data-ttu-id="62192-227">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62192-227">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="62192-228">d.</span><span class="sxs-lookup"><span data-stu-id="62192-228">d.</span></span> <span data-ttu-id="62192-229">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="62192-229">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="62192-230">e.</span><span class="sxs-lookup"><span data-stu-id="62192-230">e.</span></span> <span data-ttu-id="62192-231">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62192-231">Click **Next**.</span></span>

7. <span data-ttu-id="62192-232">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="62192-232">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="62192-234">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62192-234">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="62192-236">a.</span><span class="sxs-lookup"><span data-stu-id="62192-236">a.</span></span> <span data-ttu-id="62192-237">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="62192-237">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="62192-238">b.</span><span class="sxs-lookup"><span data-stu-id="62192-238">b.</span></span> <span data-ttu-id="62192-239">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="62192-239">Click **Complete**.</span></span>   

### <a name="creating-a-hr2day-by-merces-test-user"></a><span data-ttu-id="62192-240">Creating a HR2day by Merces test user</span><span class="sxs-lookup"><span data-stu-id="62192-240">Creating a HR2day by Merces test user</span></span>
<span data-ttu-id="62192-241">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="62192-241">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="62192-242">Please work with HR2day by Merces support team to add the users in the HR2day account.</span><span class="sxs-lookup"><span data-stu-id="62192-242">Please work with HR2day by Merces support team to add the users in the HR2day account.</span></span> 

> [!NOTE]
> <span data-ttu-id="62192-243">If you need to create an user manually, you need to contact the HR2day by Merces support team.</span><span class="sxs-lookup"><span data-stu-id="62192-243">If you need to create an user manually, you need to contact the HR2day by Merces support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62192-244">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="62192-244">Assigning the Azure AD test user</span></span>
<span data-ttu-id="62192-245">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="62192-245">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Assign User][200] 

<span data-ttu-id="62192-247">**To assign Britta Simon to HR2day by Merces, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62192-247">**To assign Britta Simon to HR2day by Merces, perform the following steps:**</span></span>

1. <span data-ttu-id="62192-248">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="62192-248">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="62192-250">In the applications list, select **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="62192-250">In the applications list, select **HR2day by Merces**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_50.png) 

3. <span data-ttu-id="62192-252">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="62192-252">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="62192-254">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62192-254">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="62192-255">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="62192-255">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="62192-257">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="62192-257">Testing Single Sign-On</span></span>
<span data-ttu-id="62192-258">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="62192-258">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="62192-259">When you click the HR2day by Merces tile in the Access Panel, you should get automatically signed-on to your HR2day by Merces application.</span><span class="sxs-lookup"><span data-stu-id="62192-259">When you click the HR2day by Merces tile in the Access Panel, you should get automatically signed-on to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62192-260">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="62192-260">Additional Resources</span></span>
* [<span data-ttu-id="62192-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62192-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62192-262">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62192-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_205.png




























