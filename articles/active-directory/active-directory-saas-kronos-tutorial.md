---
title: 'Tutorial: Azure Active Directory integration with Kronos | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kronos.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 8b3bc7fb549fc6ee8c0ecc2701a2ee718e251df2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661503"
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="64840-103">Tutorial: Azure Active Directory integration with Kronos</span><span class="sxs-lookup"><span data-stu-id="64840-103">Tutorial: Azure Active Directory integration with Kronos</span></span>
<span data-ttu-id="64840-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64840-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64840-105">Integrating Kronos with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="64840-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="64840-106">You can control in Azure AD who has access to Kronos</span><span class="sxs-lookup"><span data-stu-id="64840-106">You can control in Azure AD who has access to Kronos</span></span>
* <span data-ttu-id="64840-107">You can enable your users to automatically get signed-on to Kronos single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="64840-107">You can enable your users to automatically get signed-on to Kronos single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="64840-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="64840-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="64840-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64840-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64840-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="64840-110">Prerequisites</span></span>
<span data-ttu-id="64840-111">To configure Azure AD integration with Kronos, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="64840-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

* <span data-ttu-id="64840-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="64840-112">An Azure AD subscription</span></span>
* <span data-ttu-id="64840-113">A **Kronos Workforce Central** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="64840-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="64840-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="64840-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="64840-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="64840-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="64840-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="64840-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="64840-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64840-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64840-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="64840-118">Scenario description</span></span>
<span data-ttu-id="64840-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="64840-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="64840-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="64840-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64840-121">Adding Kronos from the gallery</span><span class="sxs-lookup"><span data-stu-id="64840-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="64840-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="64840-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-kronos-from-the-gallery"></a><span data-ttu-id="64840-123">Add Kronos from the gallery</span><span class="sxs-lookup"><span data-stu-id="64840-123">Add Kronos from the gallery</span></span>
<span data-ttu-id="64840-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="64840-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="64840-125">**To add Kronos from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="64840-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="64840-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64840-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="64840-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="64840-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="64840-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="64840-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="64840-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="64840-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="64840-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="64840-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="64840-135">In the search box, type **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="64840-135">In the search box, type **Kronos**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_01.png)

7. <span data-ttu-id="64840-137">In the results pane, select **Kronos**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="64840-137">In the results pane, select **Kronos**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64840-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="64840-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="64840-140">In this section, you configure and test Azure AD SSO with Kronos based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64840-140">In this section, you configure and test Azure AD SSO with Kronos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64840-141">For SSO to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64840-141">For SSO to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="64840-142">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span><span class="sxs-lookup"><span data-stu-id="64840-142">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="64840-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kronos.</span><span class="sxs-lookup"><span data-stu-id="64840-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kronos.</span></span>

<span data-ttu-id="64840-144">To configure and test Azure AD SSO with Kronos, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="64840-144">To configure and test Azure AD SSO with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="64840-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="64840-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="64840-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64840-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64840-147">**[Creating an Kronos test user](#creating-an-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="64840-147">**[Creating an Kronos test user](#creating-an-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="64840-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="64840-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64840-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="64840-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64840-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="64840-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="64840-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Kronos application.</span><span class="sxs-lookup"><span data-stu-id="64840-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="64840-152">Your Kronos application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="64840-152">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="64840-153">Please work with Kronos team first to identify the correct user identifier which will be mapped into the application.</span><span class="sxs-lookup"><span data-stu-id="64840-153">Please work with Kronos team first to identify the correct user identifier which will be mapped into the application.</span></span> 

<span data-ttu-id="64840-154">Also please take the guidance from Kronos team about the attribute which they want to use for this mapping.</span><span class="sxs-lookup"><span data-stu-id="64840-154">Also please take the guidance from Kronos team about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="64840-155">Microsoft recommend to use the **"NameIdentifier"** attribute as user identifier.</span><span class="sxs-lookup"><span data-stu-id="64840-155">Microsoft recommend to use the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="64840-156">You can manage the value of this attribute from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="64840-156">You can manage the value of this attribute from the **"Atrribute"** tab of the application.</span></span> 

<span data-ttu-id="64840-157">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="64840-157">The following screenshot shows an example for this.</span></span> <span data-ttu-id="64840-158">Here we have mapped the nameidentifier claim with the **userprincipalname** attribute along with the **ExtractMailPrefix** function, which provides unique user ID, which will be sent to the Kronos application in the every successful SAML Response.</span><span class="sxs-lookup"><span data-stu-id="64840-158">Here we have mapped the nameidentifier claim with the **userprincipalname** attribute along with the **ExtractMailPrefix** function, which provides unique user ID, which will be sent to the Kronos application in the every successful SAML Response.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_07.png) 

<span data-ttu-id="64840-160">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="64840-160">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="64840-161">In the classic portal, on the **Kronos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="64840-161">In the classic portal, on the **Kronos** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
     ![Configure Single Sign-On][6] 

2. <span data-ttu-id="64840-163">On the **How would you like users to sign on to Kronos** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="64840-163">On the **How would you like users to sign on to Kronos** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_03.png) 

3. <span data-ttu-id="64840-165">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="64840-165">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_04.png) 
  1. <span data-ttu-id="64840-167">In the IDENTIFIER textbox, type the URL used by your users to sign-on to your Kronos application using the following pattern: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="64840-167">In the IDENTIFIER textbox, type the URL used by your users to sign-on to your Kronos application using the following pattern: `https://<company name>.kronos.net/`</span></span>
  2. <span data-ttu-id="64840-168">In the Reply URL type the URL in the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="64840-168">In the Reply URL type the URL in the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

1. <span data-ttu-id="64840-169">On the **Configure single sign-on at Kronos** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="64840-169">On the **Configure single sign-on at Kronos** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_05.png) 
  1. <span data-ttu-id="64840-171">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="64840-171">Click **Download metadata**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="64840-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="64840-172">Click **Next**.</span></span>

2. <span data-ttu-id="64840-173">To get SSO configured for your application, contact your Kronos Account Manager and he will assist with the proper channel to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="64840-173">To get SSO configured for your application, contact your Kronos Account Manager and he will assist with the proper channel to configure SSO.</span></span> <span data-ttu-id="64840-174">Please note that you have to send email and attach downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="64840-174">Please note that you have to send email and attach downloaded metadata file.</span></span>

3. <span data-ttu-id="64840-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="64840-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

4. <span data-ttu-id="64840-177">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="64840-177">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64840-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="64840-179">Create an Azure AD test user</span></span>
<span data-ttu-id="64840-180">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64840-180">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="64840-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="64840-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="64840-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64840-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="64840-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="64840-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="64840-186">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="64840-186">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64840-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="64840-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="64840-190">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="64840-190">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="64840-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="64840-192">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="64840-193">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64840-193">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="64840-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="64840-194">Click **Next**.</span></span>

6. <span data-ttu-id="64840-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="64840-195">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="64840-197">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="64840-197">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="64840-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="64840-198">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="64840-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="64840-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="64840-200">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="64840-200">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="64840-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="64840-201">Click **Next**.</span></span>

7. <span data-ttu-id="64840-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="64840-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="64840-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="64840-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="64840-206">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="64840-206">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="64840-207">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="64840-207">Click **Complete**.</span></span>   

### <a name="create-an-kronos-test-user"></a><span data-ttu-id="64840-208">Create an Kronos test user</span><span class="sxs-lookup"><span data-stu-id="64840-208">Create an Kronos test user</span></span>
<span data-ttu-id="64840-209">In this section, you create a user called Britta Simon in Kronos.</span><span class="sxs-lookup"><span data-stu-id="64840-209">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="64840-210">Kronos application need all the users to be provisioned in the application before doing SSO.</span><span class="sxs-lookup"><span data-stu-id="64840-210">Kronos application need all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="64840-211">Please work with the Kronos Customer support associate to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="64840-211">Please work with the Kronos Customer support associate to provision all these users into the application.</span></span> 

>[!NOTE]
><span data-ttu-id="64840-212">If you need to create a user manually or batch of users, you need to contact the Kronos support team.</span><span class="sxs-lookup"><span data-stu-id="64840-212">If you need to create a user manually or batch of users, you need to contact the Kronos support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="64840-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="64840-213">Assign the Azure AD test user</span></span>
<span data-ttu-id="64840-214">In this section, you enable Britta Simon to use Azure SSO by granting her access to Kronos.</span><span class="sxs-lookup"><span data-stu-id="64840-214">In this section, you enable Britta Simon to use Azure SSO by granting her access to Kronos.</span></span>

![Assign User][200] 

<span data-ttu-id="64840-216">**To assign Britta Simon to Kronos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="64840-216">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="64840-217">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="64840-217">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="64840-219">In the applications list, select **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="64840-219">In the applications list, select **Kronos**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_kronos_50.png) 

3. <span data-ttu-id="64840-221">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="64840-221">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="64840-223">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="64840-223">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="64840-224">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="64840-224">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="64840-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="64840-226">Test single sign-on</span></span>
<span data-ttu-id="64840-227">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="64840-227">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="64840-228">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span><span class="sxs-lookup"><span data-stu-id="64840-228">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64840-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="64840-229">Additional resources</span></span>
* [<span data-ttu-id="64840-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64840-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64840-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64840-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kronos-tutorial/tutorial_general_205.png


























