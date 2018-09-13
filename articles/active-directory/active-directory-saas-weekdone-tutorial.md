---
title: 'Tutorial: Azure Active Directory integration with Weekdone | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Weekdone.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: bf73e41f02870e74404822e2b3458ca17fcba7ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669418"
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="212d9-103">Tutorial: Azure Active Directory integration with Weekdone</span><span class="sxs-lookup"><span data-stu-id="212d9-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>
<span data-ttu-id="212d9-104">The objective of this tutorial is to show you how to integrate Weekdone with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="212d9-104">The objective of this tutorial is to show you how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="212d9-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="212d9-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="212d9-106">You can control in Azure AD who has access to Weekdone</span><span class="sxs-lookup"><span data-stu-id="212d9-106">You can control in Azure AD who has access to Weekdone</span></span>
* <span data-ttu-id="212d9-107">You can enable your users to automatically get signed-on to Weekdone single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="212d9-107">You can enable your users to automatically get signed-on to Weekdone single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="212d9-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="212d9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="212d9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="212d9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="212d9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="212d9-110">Prerequisites</span></span>
<span data-ttu-id="212d9-111">To configure Azure AD integration with Weekdone, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="212d9-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

* <span data-ttu-id="212d9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="212d9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="212d9-113">A Weekdone single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="212d9-113">A Weekdone single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="212d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="212d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="212d9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="212d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="212d9-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="212d9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="212d9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial [h](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="212d9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial [h](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="212d9-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="212d9-118">Scenario Description</span></span>
<span data-ttu-id="212d9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="212d9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="212d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="212d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="212d9-121">Adding Weekdone from the gallery</span><span class="sxs-lookup"><span data-stu-id="212d9-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="212d9-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="212d9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="212d9-123">Adding Weekdone from the gallery</span><span class="sxs-lookup"><span data-stu-id="212d9-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="212d9-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="212d9-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="212d9-125">**To add Weekdone from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="212d9-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="212d9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="212d9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="212d9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="212d9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="212d9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="212d9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="212d9-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="212d9-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="212d9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="212d9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="212d9-135">In the search box, type **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="212d9-135">In the search box, type **Weekdone**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_01.png)
7. <span data-ttu-id="212d9-137">In the results pane, select **Weekdone**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="212d9-137">In the results pane, select **Weekdone**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="212d9-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="212d9-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="212d9-140">The objective of this section is to show you how to configure and test Azure AD SSO with Weekdone based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="212d9-140">The objective of this section is to show you how to configure and test Azure AD SSO with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="212d9-141">For SSO to work, Azure AD needs to know what the counterpart user in Weekdone to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="212d9-141">For SSO to work, Azure AD needs to know what the counterpart user in Weekdone to an user in Azure AD is.</span></span> <span data-ttu-id="212d9-142">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span><span class="sxs-lookup"><span data-stu-id="212d9-142">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="212d9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Weekdone.</span><span class="sxs-lookup"><span data-stu-id="212d9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Weekdone.</span></span>

<span data-ttu-id="212d9-144">To configure and test Azure AD SSO with Weekdone, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="212d9-144">To configure and test Azure AD SSO with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="212d9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="212d9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="212d9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="212d9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="212d9-147">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="212d9-147">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="212d9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="212d9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="212d9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="212d9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="212d9-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="212d9-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="212d9-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Weekdone application.</span><span class="sxs-lookup"><span data-stu-id="212d9-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Weekdone application.</span></span>

<span data-ttu-id="212d9-152">**To configure Azure AD SSO with Weekdone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="212d9-152">**To configure Azure AD SSO with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="212d9-153">In the Azure classic portal, on the **Weekdone** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="212d9-153">In the Azure classic portal, on the **Weekdone** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="212d9-155">On the **How would you like users to sign on to Weekdone** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-155">On the **How would you like users to sign on to Weekdone** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_03.png) 
3. <span data-ttu-id="212d9-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="212d9-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_04.png) 

   1. <span data-ttu-id="212d9-159">In the **Reply URL** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure"**.</span><span class="sxs-lookup"><span data-stu-id="212d9-159">In the **Reply URL** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure"**.</span></span>
   2. <span data-ttu-id="212d9-160">In the **Identifier** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure/metadata"**.</span><span class="sxs-lookup"><span data-stu-id="212d9-160">In the **Identifier** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure/metadata"**.</span></span>
   3. <span data-ttu-id="212d9-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-161">Click **Next**.</span></span>
4. <span data-ttu-id="212d9-162">If you want to configure the application in **SP initiated mode**, on the **Configure App Settings** dialog page, select **“Show advanced settings (optional)”**, and then enter the **Sign On URL** and **Identifier**, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-162">If you want to configure the application in **SP initiated mode**, on the **Configure App Settings** dialog page, select **“Show advanced settings (optional)”**, and then enter the **Sign On URL** and **Identifier**, then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_06.png) 
   
   1. <span data-ttu-id="212d9-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Weekdone application using the following pattern: **“https://weekdone.com/a/azure”**.</span><span class="sxs-lookup"><span data-stu-id="212d9-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Weekdone application using the following pattern: **“https://weekdone.com/a/azure”**.</span></span>
   2. <span data-ttu-id="212d9-165">In the **Identifier** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure/metadata"**.</span><span class="sxs-lookup"><span data-stu-id="212d9-165">In the **Identifier** textbox, type the URL in the following pattern: **"https://weekdone.com/a/azure/metadata"**.</span></span>
   3. <span data-ttu-id="212d9-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-166">Click **Next**.</span></span>
2. <span data-ttu-id="212d9-167">On the **Configure single sign-on at Weekdone** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="212d9-167">On the **Configure single sign-on at Weekdone** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_05.png) 
   1. <span data-ttu-id="212d9-169">Click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="212d9-169">Click **Download certificate**, and then save the certificate file on your computer.</span></span>
   2. <span data-ttu-id="212d9-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-170">Click **Next**.</span></span>
    
3. <span data-ttu-id="212d9-171">To get SSO configured for your application, contact your Weekdone support team via hello@weekdone.com.</span><span class="sxs-lookup"><span data-stu-id="212d9-171">To get SSO configured for your application, contact your Weekdone support team via hello@weekdone.com.</span></span> 
4. <span data-ttu-id="212d9-172">Attach the downloaded certificate file to your mail and share the metadata urls (ISSUER URL, SAML SSO URL and SINGLE SIGN-OUT SERVICE URL) with Weekdone team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="212d9-172">Attach the downloaded certificate file to your mail and share the metadata urls (ISSUER URL, SAML SSO URL and SINGLE SIGN-OUT SERVICE URL) with Weekdone team to set up SSO on their side.</span></span>
5. <span data-ttu-id="212d9-173">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-173">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
6. <span data-ttu-id="212d9-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="212d9-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="212d9-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="212d9-177">Create an Azure AD test user</span></span>
<span data-ttu-id="212d9-178">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="212d9-178">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="212d9-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="212d9-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="212d9-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="212d9-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_09.png) 
    
2. <span data-ttu-id="212d9-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="212d9-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="212d9-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="212d9-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 
    
4. <span data-ttu-id="212d9-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="212d9-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 
    
5. <span data-ttu-id="212d9-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="212d9-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="212d9-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="212d9-190">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="212d9-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="212d9-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="212d9-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-192">Click **Next**.</span></span>
    
6. <span data-ttu-id="212d9-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="212d9-193">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="212d9-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="212d9-195">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="212d9-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="212d9-196">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="212d9-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="212d9-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="212d9-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="212d9-198">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="212d9-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="212d9-199">Click **Next**.</span></span>
  
7. <span data-ttu-id="212d9-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="212d9-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_07.png) 
    
8. <span data-ttu-id="212d9-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="212d9-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="212d9-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="212d9-204">Write down the value of the **New Password**.</span></span> 
   2. <span data-ttu-id="212d9-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="212d9-205">Click **Complete**.</span></span>   

### <a name="create-a-weekdone-test-user"></a><span data-ttu-id="212d9-206">Create a Weekdone test user</span><span class="sxs-lookup"><span data-stu-id="212d9-206">Create a Weekdone test user</span></span>
<span data-ttu-id="212d9-207">The objective of this section is to create a user called Britta Simon in Weekdone.</span><span class="sxs-lookup"><span data-stu-id="212d9-207">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="212d9-208">Weekdone supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="212d9-208">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="212d9-209">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="212d9-209">There is no action item for you in this section.</span></span> <span data-ttu-id="212d9-210">A new user will be created during an attempt to access Weekdone if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="212d9-210">A new user will be created during an attempt to access Weekdone if it doesn't exist yet.</span></span> <span data-ttu-id="212d9-211">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="212d9-211">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="212d9-212">If you need to create an user manually, you need to contact the Weekdone support team via hello@weekdone.com.</span><span class="sxs-lookup"><span data-stu-id="212d9-212">If you need to create an user manually, you need to contact the Weekdone support team via hello@weekdone.com.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="212d9-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="212d9-213">Assign the Azure AD test user</span></span>
<span data-ttu-id="212d9-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Weekdone.</span><span class="sxs-lookup"><span data-stu-id="212d9-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Weekdone.</span></span>

![Assign User][200] 

<span data-ttu-id="212d9-216">**To assign Britta Simon to Weekdone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="212d9-216">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="212d9-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="212d9-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="212d9-219">In the applications list, select **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="212d9-219">In the applications list, select **Weekdone**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_50.png) 
3. <span data-ttu-id="212d9-221">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="212d9-221">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="212d9-223">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="212d9-223">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="212d9-224">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="212d9-224">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="212d9-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="212d9-226">Test single sign-on</span></span>
<span data-ttu-id="212d9-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="212d9-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="212d9-228">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span><span class="sxs-lookup"><span data-stu-id="212d9-228">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="212d9-229">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="212d9-229">Additional Resources</span></span>
* [<span data-ttu-id="212d9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="212d9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="212d9-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="212d9-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-weekdone-tutorial/tutorial_general_205.png


























