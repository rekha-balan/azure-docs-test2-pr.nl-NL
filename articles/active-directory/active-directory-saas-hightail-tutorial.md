---
title: 'Tutorial: Azure Active Directory integration with Hightail | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Hightail.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 65ebe1c3dd4e34d05e2e50216900e5dbf5dc519f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552715"
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="ff6f8-103">Tutorial: Azure Active Directory integration with Hightail</span><span class="sxs-lookup"><span data-stu-id="ff6f8-103">Tutorial: Azure Active Directory integration with Hightail</span></span>
<span data-ttu-id="ff6f8-104">The objective of this tutorial is to show you how to integrate Hightail with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff6f8-104">The objective of this tutorial is to show you how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff6f8-105">Integrating Hightail with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ff6f8-106">You can control in Azure AD who has access to Hightail</span><span class="sxs-lookup"><span data-stu-id="ff6f8-106">You can control in Azure AD who has access to Hightail</span></span>
* <span data-ttu-id="ff6f8-107">You can enable your users to automatically get signed-on to Hightail single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ff6f8-107">You can enable your users to automatically get signed-on to Hightail single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ff6f8-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ff6f8-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ff6f8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff6f8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff6f8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff6f8-110">Prerequisites</span></span>
<span data-ttu-id="ff6f8-111">To configure Azure AD integration with Hightail, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

* <span data-ttu-id="ff6f8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ff6f8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ff6f8-113">A Hightail single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ff6f8-113">A Hightail single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ff6f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="ff6f8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ff6f8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ff6f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff6f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff6f8-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ff6f8-118">Scenario Description</span></span>
<span data-ttu-id="ff6f8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ff6f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff6f8-121">Adding Hightail from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff6f8-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="ff6f8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff6f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-hightail-from-the-gallery"></a><span data-ttu-id="ff6f8-123">Add Hightail from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff6f8-123">Add Hightail from the gallery</span></span>
<span data-ttu-id="ff6f8-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff6f8-125">**To add Hightail from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff6f8-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff6f8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ff6f8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ff6f8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ff6f8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ff6f8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ff6f8-135">In the search box, type **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-135">In the search box, type **Hightail**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_01.png)
7. <span data-ttu-id="ff6f8-137">In the results pane, select **Hightail**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-137">In the results pane, select **Hightail**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ff6f8-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff6f8-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ff6f8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ff6f8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff6f8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail to an user in Azure AD is.</span></span> <span data-ttu-id="ff6f8-142">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-142">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="ff6f8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Hightail.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Hightail.</span></span>

<span data-ttu-id="ff6f8-144">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-144">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff6f8-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff6f8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff6f8-147">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-147">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ff6f8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff6f8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ff6f8-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff6f8-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="ff6f8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Hightail application.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="ff6f8-152">Hightail application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-152">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ff6f8-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="ff6f8-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="ff6f8-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_51.png) 

<span data-ttu-id="ff6f8-157">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff6f8-157">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="ff6f8-158">In the Azure classic portal, on the **Hightail** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-158">In the Azure classic portal, on the **Hightail** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_81.png) 
2. <span data-ttu-id="ff6f8-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="ff6f8-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ff6f8-161">Attribute Name</span></span> | <span data-ttu-id="ff6f8-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ff6f8-162">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="ff6f8-163">FirstName</span><span class="sxs-lookup"><span data-stu-id="ff6f8-163">FirstName</span></span> |<span data-ttu-id="ff6f8-164">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ff6f8-164">user.givenname</span></span> |
   | <span data-ttu-id="ff6f8-165">LastName</span><span class="sxs-lookup"><span data-stu-id="ff6f8-165">LastName</span></span> |<span data-ttu-id="ff6f8-166">user.surname</span><span class="sxs-lookup"><span data-stu-id="ff6f8-166">user.surname</span></span> |
   | <span data-ttu-id="ff6f8-167">Email</span><span class="sxs-lookup"><span data-stu-id="ff6f8-167">Email</span></span> |<span data-ttu-id="ff6f8-168">user.mail</span><span class="sxs-lookup"><span data-stu-id="ff6f8-168">user.mail</span></span> |
   | <span data-ttu-id="ff6f8-169">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="ff6f8-169">UserIdentity</span></span> |<span data-ttu-id="ff6f8-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="ff6f8-170">user.mail</span></span> |
   
    1. <span data-ttu-id="ff6f8-171">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-171">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_82.png) 
    2. <span data-ttu-id="ff6f8-173">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-173">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
    3. <span data-ttu-id="ff6f8-174">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-174">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
    4. <span data-ttu-id="ff6f8-175">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-175">Click **Complete**.</span></span>    

1. <span data-ttu-id="ff6f8-176">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-176">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_83.png)  
2. <span data-ttu-id="ff6f8-178">On the **How would you like users to sign on to Hightail** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-178">On the **How would you like users to sign on to Hightail** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_03.png) 
3. <span data-ttu-id="ff6f8-180">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-180">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_04.png) 
    1. <span data-ttu-id="ff6f8-182">In the **Reply URL** textbox, type the URL in the following pattern: **"https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse"**</span><span class="sxs-lookup"><span data-stu-id="ff6f8-182">In the **Reply URL** textbox, type the URL in the following pattern: **"https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse"**</span></span>
    2. <span data-ttu-id="ff6f8-183">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-183">Click **Next**.</span></span>

1. <span data-ttu-id="ff6f8-184">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-184">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_06.png) 
    1. <span data-ttu-id="ff6f8-186">In the Sign On URL textbox, type the URL used by your users to sign-on to your Hightail application using the following pattern: **https://www.hightail.com/loginSSO**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-186">In the Sign On URL textbox, type the URL used by your users to sign-on to your Hightail application using the following pattern: **https://www.hightail.com/loginSSO**.</span></span> <span data-ttu-id="ff6f8-187">This is the common Login page for all the customers who wish to use SSO.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-187">This is the common Login page for all the customers who wish to use SSO.</span></span>
    2. <span data-ttu-id="ff6f8-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-188">Click **Next**.</span></span>
2. <span data-ttu-id="ff6f8-189">On the **Configure single sign-on at Hightail** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-189">On the **Configure single sign-on at Hightail** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_05.png) 
    1. <span data-ttu-id="ff6f8-191">Click **Download certificate**, and then save the base-64 encoded certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-191">Click **Download certificate**, and then save the base-64 encoded certificate file on your computer.</span></span>
    2. <span data-ttu-id="ff6f8-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-192">Click **Next**.</span></span>
    >[!NOTE] 
    ><span data-ttu-id="ff6f8-193">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can leverage Single Sign On functionality.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-193">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can leverage Single Sign On functionality.</span></span>
    >

1. <span data-ttu-id="ff6f8-194">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-194">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    1. <span data-ttu-id="ff6f8-195">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-195">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 
    2. <span data-ttu-id="ff6f8-197">Select the checkbox of **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-197">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 
    3. <span data-ttu-id="ff6f8-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 
    4. <span data-ttu-id="ff6f8-201">Copy Remote Login URL from Azure AD to **SAML Authority (Identity Provider)** in Hightail.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-201">Copy Remote Login URL from Azure AD to **SAML Authority (Identity Provider)** in Hightail.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_005.png)

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)
    5. <span data-ttu-id="ff6f8-204">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-204">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="ff6f8-205">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-205">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)
    6. <span data-ttu-id="ff6f8-207">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox as shown in step 4.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-207">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox as shown in step 4.</span></span> 
    7. <span data-ttu-id="ff6f8-208">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-208">Click **Save**.</span></span>

1. <span data-ttu-id="ff6f8-209">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-209">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
2. <span data-ttu-id="ff6f8-211">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-211">On the **Single sign-on confirmation** page, click **Complete**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ff6f8-213">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff6f8-213">Create an Azure AD test user</span></span>
<span data-ttu-id="ff6f8-214">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-214">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="ff6f8-215">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-215">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="ff6f8-217">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff6f8-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff6f8-218">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-218">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="ff6f8-220">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-220">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ff6f8-221">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-221">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="ff6f8-223">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-223">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="ff6f8-225">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-225">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_05.png) 
   
    1. <span data-ttu-id="ff6f8-227">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-227">As **Type Of User**, select **New user in your organization**.</span></span>
    2. <span data-ttu-id="ff6f8-228">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-228">In the **User Name** textbox, type **BrittaSimon**.</span></span>
    3. <span data-ttu-id="ff6f8-229">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-229">Click **Next**.</span></span>
6. <span data-ttu-id="ff6f8-230">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-230">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="ff6f8-232">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-232">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="ff6f8-233">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-233">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="ff6f8-234">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-234">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="ff6f8-235">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-235">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="ff6f8-236">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-236">Click **Next**.</span></span>
7. <span data-ttu-id="ff6f8-237">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-237">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="ff6f8-239">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff6f8-239">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/create_aaduser_08.png) 
   
    1. <span data-ttu-id="ff6f8-241">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-241">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="ff6f8-242">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-242">Click **Complete**.</span></span>   

### <a name="create-a-hightail-test-user"></a><span data-ttu-id="ff6f8-243">Create a Hightail test user</span><span class="sxs-lookup"><span data-stu-id="ff6f8-243">Create a Hightail test user</span></span>
<span data-ttu-id="ff6f8-244">The objective of this section is to create a user called Britta Simon in Hightail.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-244">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="ff6f8-245">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-245">There is no action item for you in this section.</span></span> <span data-ttu-id="ff6f8-246">Hightail supports just-in-time user provisioning based on the custom claims.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-246">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="ff6f8-247">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-247">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="ff6f8-248">If you need to create an user manually, you need to contact the Hightail support team via [support@hightail.com](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="ff6f8-248">If you need to create an user manually, you need to contact the Hightail support team via [support@hightail.com](mailto:support@hightail.com).</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ff6f8-249">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff6f8-249">Assign the Azure AD test user</span></span>
<span data-ttu-id="ff6f8-250">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Hightail.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-250">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Hightail.</span></span>

![Assign User][200] 

<span data-ttu-id="ff6f8-252">**To assign Britta Simon to Hightail, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff6f8-252">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="ff6f8-253">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-253">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="ff6f8-255">In the applications list, select **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-255">In the applications list, select **Hightail**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_hightail_50.png) 
3. <span data-ttu-id="ff6f8-257">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-257">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="ff6f8-259">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-259">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ff6f8-260">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-260">In the toolbar on the bottom, click **Assign**.</span></span>

![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ff6f8-262">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ff6f8-262">Test Single Sign-On</span></span>
<span data-ttu-id="ff6f8-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff6f8-264">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span><span class="sxs-lookup"><span data-stu-id="ff6f8-264">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff6f8-265">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ff6f8-265">Additional Resources</span></span>
* [<span data-ttu-id="ff6f8-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff6f8-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff6f8-267">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff6f8-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_205.png




































