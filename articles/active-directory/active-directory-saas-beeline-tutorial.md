---
title: 'Tutorial: Azure Active Directory integration with Beeline | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Beeline.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 2bf37547cb693a4ced0b1a4e2decfc4fab2d9fd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540670"
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="58c9f-103">Tutorial: Azure Active Directory integration with BeeLine</span><span class="sxs-lookup"><span data-stu-id="58c9f-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>
<span data-ttu-id="58c9f-104">In this tutorial, you learn how to integrate Beeline with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58c9f-104">In this tutorial, you learn how to integrate Beeline with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58c9f-105">Integrating Beeline with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="58c9f-105">Integrating Beeline with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="58c9f-106">You can control in Azure AD who has access to Beeline</span><span class="sxs-lookup"><span data-stu-id="58c9f-106">You can control in Azure AD who has access to Beeline</span></span>
* <span data-ttu-id="58c9f-107">You can enable your users to automatically get signed-on to Beeline (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="58c9f-107">You can enable your users to automatically get signed-on to Beeline (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="58c9f-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="58c9f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="58c9f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58c9f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58c9f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="58c9f-110">Prerequisites</span></span>
<span data-ttu-id="58c9f-111">To configure Azure AD integration with Beeline, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="58c9f-111">To configure Azure AD integration with Beeline, you need the following items:</span></span>

* <span data-ttu-id="58c9f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="58c9f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="58c9f-113">A Beeline single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="58c9f-113">A Beeline single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58c9f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="58c9f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="58c9f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="58c9f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="58c9f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="58c9f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="58c9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58c9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58c9f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="58c9f-118">Scenario description</span></span>
<span data-ttu-id="58c9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="58c9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58c9f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="58c9f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58c9f-121">Adding Beeline from the gallery</span><span class="sxs-lookup"><span data-stu-id="58c9f-121">Adding Beeline from the gallery</span></span>
2. <span data-ttu-id="58c9f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58c9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="58c9f-123">Adding Beeline from the gallery</span><span class="sxs-lookup"><span data-stu-id="58c9f-123">Adding Beeline from the gallery</span></span>
<span data-ttu-id="58c9f-124">To configure the integration of Beeline into Azure AD, you need to add Beeline from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="58c9f-124">To configure the integration of Beeline into Azure AD, you need to add Beeline from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58c9f-125">**To add Beeline from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58c9f-125">**To add Beeline from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58c9f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="58c9f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="58c9f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="58c9f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="58c9f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="58c9f-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="58c9f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="58c9f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="58c9f-135">In the search box, type **Beeline**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-135">In the search box, type **Beeline**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_01.png)
7. <span data-ttu-id="58c9f-137">In the results pane, select **Beeline**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-137">In the results pane, select **Beeline**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_06.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58c9f-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58c9f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58c9f-140">In this section, you configure and test Azure AD single sign-on with Beeline based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="58c9f-140">In this section, you configure and test Azure AD single sign-on with Beeline based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58c9f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Beeline is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58c9f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Beeline is to a user in Azure AD.</span></span> <span data-ttu-id="58c9f-142">In other words, a link relationship between an Azure AD user and the related user in Beeline needs to be established.</span><span class="sxs-lookup"><span data-stu-id="58c9f-142">In other words, a link relationship between an Azure AD user and the related user in Beeline needs to be established.</span></span>
<span data-ttu-id="58c9f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Beeline.</span><span class="sxs-lookup"><span data-stu-id="58c9f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Beeline.</span></span>

<span data-ttu-id="58c9f-144">To configure and test Azure AD single sign-on with Beeline, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="58c9f-144">To configure and test Azure AD single sign-on with Beeline, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58c9f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="58c9f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58c9f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58c9f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58c9f-147">**[Creating an Beeline test user](#creating-an-beeline-test-user)** - to have a counterpart of Britta Simon in Beeline that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="58c9f-147">**[Creating an Beeline test user](#creating-an-beeline-test-user)** - to have a counterpart of Britta Simon in Beeline that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="58c9f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="58c9f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58c9f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="58c9f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58c9f-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58c9f-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="58c9f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Beeline application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Beeline application.</span></span>

<span data-ttu-id="58c9f-152">Your Beeline application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="58c9f-152">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="58c9f-153">Please work with Beeline team first to identify the correct user identifier which will be mapped into the application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-153">Please work with Beeline team first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="58c9f-154">Also please take the guidance from Beeline team about the attribute which they want to use for this mapping.</span><span class="sxs-lookup"><span data-stu-id="58c9f-154">Also please take the guidance from Beeline team about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="58c9f-155">Microsoft recommend to use the **"NameIdentifier"** attribute as user identifier.</span><span class="sxs-lookup"><span data-stu-id="58c9f-155">Microsoft recommend to use the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="58c9f-156">You can manage the value of this attribute from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-156">You can manage the value of this attribute from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="58c9f-157">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="58c9f-157">The following screenshot shows an example for this.</span></span> <span data-ttu-id="58c9f-158">Here we have mapped the nameidentifier claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span><span class="sxs-lookup"><span data-stu-id="58c9f-158">Here we have mapped the nameidentifier claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_07.png) 

<span data-ttu-id="58c9f-160">**To configure Azure AD single sign-on with Beeline, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58c9f-160">**To configure Azure AD single sign-on with Beeline, perform the following steps:**</span></span>

1. <span data-ttu-id="58c9f-161">In the classic portal, on the **Beeline** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="58c9f-161">In the classic portal, on the **Beeline** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
     ![Configure Single Sign-On][6] 
2. <span data-ttu-id="58c9f-163">On the **How would you like users to sign on to Beeline** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-163">On the **How would you like users to sign on to Beeline** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_03.png) 
3. <span data-ttu-id="58c9f-165">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="58c9f-165">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_04.png) 

    <span data-ttu-id="58c9f-167">a.</span><span class="sxs-lookup"><span data-stu-id="58c9f-167">a.</span></span> <span data-ttu-id="58c9f-168">In the **Identifier** textbox, type the URL used by your users to sign-on to your Beeline application using the following pattern: `https://projects.beeline.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="58c9f-168">In the **Identifier** textbox, type the URL used by your users to sign-on to your Beeline application using the following pattern: `https://projects.beeline.net/<instance name>`</span></span>

    <span data-ttu-id="58c9f-169">b.</span><span class="sxs-lookup"><span data-stu-id="58c9f-169">b.</span></span> <span data-ttu-id="58c9f-170">In the Reply URL type the URL in the following pattern: `https://projects.beeline.net/<instance name>/SSO_External.ashx` or `https://projects.beeline.net/<company name>/SSO_External.ashx`</span><span class="sxs-lookup"><span data-stu-id="58c9f-170">In the Reply URL type the URL in the following pattern: `https://projects.beeline.net/<instance name>/SSO_External.ashx` or `https://projects.beeline.net/<company name>/SSO_External.ashx`</span></span>


1. <span data-ttu-id="58c9f-171">On the **Configure single sign-on at Beeline** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58c9f-171">On the **Configure single sign-on at Beeline** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_05.png) 
   
    <span data-ttu-id="58c9f-173">a.</span><span class="sxs-lookup"><span data-stu-id="58c9f-173">a.</span></span> <span data-ttu-id="58c9f-174">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="58c9f-174">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="58c9f-175">b.</span><span class="sxs-lookup"><span data-stu-id="58c9f-175">b.</span></span> <span data-ttu-id="58c9f-176">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-176">Click **Next**.</span></span>
2. <span data-ttu-id="58c9f-177">To get SSO configured for your application, contact Beeline Support team and they will assist to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="58c9f-177">To get SSO configured for your application, contact Beeline Support team and they will assist to configure SSO.</span></span> <span data-ttu-id="58c9f-178">Please note that you have to send email and attach downloaded metadata file and also provide the Entity ID and Single Sign Out Service URL.</span><span class="sxs-lookup"><span data-stu-id="58c9f-178">Please note that you have to send email and attach downloaded metadata file and also provide the Entity ID and Single Sign Out Service URL.</span></span>
3. <span data-ttu-id="58c9f-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="58c9f-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58c9f-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="58c9f-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="58c9f-184">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58c9f-184">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="58c9f-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58c9f-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58c9f-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="58c9f-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="58c9f-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="58c9f-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="58c9f-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="58c9f-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58c9f-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="58c9f-196">a.</span><span class="sxs-lookup"><span data-stu-id="58c9f-196">a.</span></span> <span data-ttu-id="58c9f-197">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="58c9f-197">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="58c9f-198">b.</span><span class="sxs-lookup"><span data-stu-id="58c9f-198">b.</span></span> <span data-ttu-id="58c9f-199">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-199">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="58c9f-200">c.</span><span class="sxs-lookup"><span data-stu-id="58c9f-200">c.</span></span> <span data-ttu-id="58c9f-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-201">Click **Next**.</span></span>
6. <span data-ttu-id="58c9f-202">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58c9f-202">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="58c9f-204">a.</span><span class="sxs-lookup"><span data-stu-id="58c9f-204">a.</span></span> <span data-ttu-id="58c9f-205">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-205">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="58c9f-206">b.</span><span class="sxs-lookup"><span data-stu-id="58c9f-206">b.</span></span> <span data-ttu-id="58c9f-207">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-207">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="58c9f-208">c.</span><span class="sxs-lookup"><span data-stu-id="58c9f-208">c.</span></span> <span data-ttu-id="58c9f-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="58c9f-210">d.</span><span class="sxs-lookup"><span data-stu-id="58c9f-210">d.</span></span> <span data-ttu-id="58c9f-211">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-211">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="58c9f-212">e.</span><span class="sxs-lookup"><span data-stu-id="58c9f-212">e.</span></span> <span data-ttu-id="58c9f-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-213">Click **Next**.</span></span>

7. <span data-ttu-id="58c9f-214">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-214">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="58c9f-216">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58c9f-216">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="58c9f-218">a.</span><span class="sxs-lookup"><span data-stu-id="58c9f-218">a.</span></span> <span data-ttu-id="58c9f-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-219">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="58c9f-220">b.</span><span class="sxs-lookup"><span data-stu-id="58c9f-220">b.</span></span> <span data-ttu-id="58c9f-221">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-221">Click **Complete**.</span></span>   

### <a name="creating-an-beeline-test-user"></a><span data-ttu-id="58c9f-222">Creating an Beeline test user</span><span class="sxs-lookup"><span data-stu-id="58c9f-222">Creating an Beeline test user</span></span>
<span data-ttu-id="58c9f-223">In this section, you create a user called Britta Simon in Beeline.</span><span class="sxs-lookup"><span data-stu-id="58c9f-223">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="58c9f-224">Beeline application need all the users to be provisioned in the application before doing Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="58c9f-224">Beeline application need all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="58c9f-225">So please work with the Beeline Customer support associate to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-225">So please work with the Beeline Customer support associate to provision all these users into the application.</span></span> 

> [!NOTE]
> <span data-ttu-id="58c9f-226">If you need to create a user manually or batch of users, you need to contact the Beeline support team.</span><span class="sxs-lookup"><span data-stu-id="58c9f-226">If you need to create a user manually or batch of users, you need to contact the Beeline support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="58c9f-227">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="58c9f-227">Assigning the Azure AD test user</span></span>
<span data-ttu-id="58c9f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Beeline.</span><span class="sxs-lookup"><span data-stu-id="58c9f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Beeline.</span></span>

![Assign User][200] 

<span data-ttu-id="58c9f-230">**To assign Britta Simon to Beeline, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58c9f-230">**To assign Britta Simon to Beeline, perform the following steps:**</span></span>

1. <span data-ttu-id="58c9f-231">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="58c9f-231">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="58c9f-233">In the applications list, select **Beeline**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-233">In the applications list, select **Beeline**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_beeline_50.png) 
3. <span data-ttu-id="58c9f-235">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-235">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="58c9f-237">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-237">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="58c9f-238">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="58c9f-238">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="58c9f-240">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="58c9f-240">Testing single sign-on</span></span>
<span data-ttu-id="58c9f-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="58c9f-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="58c9f-242">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span><span class="sxs-lookup"><span data-stu-id="58c9f-242">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58c9f-243">Additional resources</span><span class="sxs-lookup"><span data-stu-id="58c9f-243">Additional resources</span></span>
* [<span data-ttu-id="58c9f-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58c9f-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58c9f-245">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58c9f-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-beeline-tutorial/tutorial_general_205.png


























