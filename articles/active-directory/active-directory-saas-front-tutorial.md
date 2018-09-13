---
title: 'Tutorial: Azure Active Directory integration with Front | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Front.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: jeedes
ms.openlocfilehash: f95cc2ea892ede1ed8894a3479218fb13729fa79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550869"
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="390b9-103">Tutorial: Azure Active Directory integration with Front</span><span class="sxs-lookup"><span data-stu-id="390b9-103">Tutorial: Azure Active Directory integration with Front</span></span>
<span data-ttu-id="390b9-104">The objective of this tutorial is to show you how to integrate Front with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="390b9-104">The objective of this tutorial is to show you how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="390b9-105">Integrating Front with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="390b9-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="390b9-106">You can control in Azure AD who has access to Front</span><span class="sxs-lookup"><span data-stu-id="390b9-106">You can control in Azure AD who has access to Front</span></span>
* <span data-ttu-id="390b9-107">You can enable your users to automatically get signed-on to Front single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="390b9-107">You can enable your users to automatically get signed-on to Front single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="390b9-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="390b9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="390b9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="390b9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="390b9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="390b9-110">Prerequisites</span></span>
<span data-ttu-id="390b9-111">To configure Azure AD integration with Front, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="390b9-111">To configure Azure AD integration with Front, you need the following items:</span></span>

* <span data-ttu-id="390b9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="390b9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="390b9-113">A Front single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="390b9-113">A Front single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="390b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="390b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="390b9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="390b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="390b9-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="390b9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="390b9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="390b9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="390b9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="390b9-118">Scenario description</span></span>
<span data-ttu-id="390b9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="390b9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="390b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="390b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="390b9-121">Adding Front from the gallery</span><span class="sxs-lookup"><span data-stu-id="390b9-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="390b9-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="390b9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="390b9-123">Adding Front from the gallery</span><span class="sxs-lookup"><span data-stu-id="390b9-123">Adding Front from the gallery</span></span>
<span data-ttu-id="390b9-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="390b9-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="390b9-125">**To add Front from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="390b9-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="390b9-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="390b9-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="390b9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="390b9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="390b9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="390b9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="390b9-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="390b9-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="390b9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="390b9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="390b9-135">In the search box, type **Front**.</span><span class="sxs-lookup"><span data-stu-id="390b9-135">In the search box, type **Front**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_01.png)
7. <span data-ttu-id="390b9-137">In the results panel, select **Front**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="390b9-137">In the results panel, select **Front**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="390b9-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="390b9-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="390b9-140">The objective of this section is to show you how to configure and test Azure AD SSO with Front based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="390b9-140">The objective of this section is to show you how to configure and test Azure AD SSO with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="390b9-141">For SSO to work, Azure AD needs to know what the counterpart user in Front to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="390b9-141">For SSO to work, Azure AD needs to know what the counterpart user in Front to an user in Azure AD is.</span></span> <span data-ttu-id="390b9-142">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span><span class="sxs-lookup"><span data-stu-id="390b9-142">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="390b9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Front.</span><span class="sxs-lookup"><span data-stu-id="390b9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Front.</span></span>

<span data-ttu-id="390b9-144">To configure and test Azure AD SSO with Front, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="390b9-144">To configure and test Azure AD SSO with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="390b9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="390b9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="390b9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="390b9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="390b9-147">**[Creating a Front test user](#creating-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="390b9-147">**[Creating a Front test user](#creating-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="390b9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="390b9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="390b9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="390b9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="390b9-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="390b9-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="390b9-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Front application.</span><span class="sxs-lookup"><span data-stu-id="390b9-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="390b9-152">**To configure Azure AD SSO with Front, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="390b9-152">**To configure Azure AD SSO with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="390b9-153">In the classic portal, on the **Front** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="390b9-153">In the classic portal, on the **Front** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="390b9-155">On the **How would you like users to sign on to Front** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-155">On the **How would you like users to sign on to Front** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_03.png)
3. <span data-ttu-id="390b9-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="390b9-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_04.png)
  1. <span data-ttu-id="390b9-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`.</span><span class="sxs-lookup"><span data-stu-id="390b9-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`.</span></span>
  2. <span data-ttu-id="390b9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="390b9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com/sso/saml/callback`</span></span>
  3. <span data-ttu-id="390b9-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-161">Click **Next**.</span></span>
4. <span data-ttu-id="390b9-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_05.png)
   
  1. <span data-ttu-id="390b9-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="390b9-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`</span></span>
  2. <span data-ttu-id="390b9-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-165">Click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="390b9-166">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="390b9-166">Please note that these are not the real values.</span></span> <span data-ttu-id="390b9-167">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="390b9-167">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="390b9-168">To get these values, you can refer **step 12** for details or contact Front via [support@frontapp.com](emailTo:support@frontapp.com).</span><span class="sxs-lookup"><span data-stu-id="390b9-168">To get these values, you can refer **step 12** for details or contact Front via [support@frontapp.com](emailTo:support@frontapp.com).</span></span>
   >  
5. <span data-ttu-id="390b9-169">On the **Configure single sign-on at Front** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="390b9-169">On the **Configure single sign-on at Front** page, perform the following steps and click **Next**:</span></span>
   
 ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_06.png) 
 1. <span data-ttu-id="390b9-171">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="390b9-171">Click **Download certificate**, and then save the file on your computer.</span></span>
 2. <span data-ttu-id="390b9-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-172">Click **Next**.</span></span>
6. <span data-ttu-id="390b9-173">Sign-on to your Front tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="390b9-173">Sign-on to your Front tenant as an administrator.</span></span>
7. <span data-ttu-id="390b9-174">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span><span class="sxs-lookup"><span data-stu-id="390b9-174">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_000.png)
8. <span data-ttu-id="390b9-176">Click **Single Sign On** link.</span><span class="sxs-lookup"><span data-stu-id="390b9-176">Click **Single Sign On** link.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_001.png)
9. <span data-ttu-id="390b9-178">Select **SAML** in the drop down list of **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="390b9-178">Select **SAML** in the drop down list of **Single Sign On**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_002.png)
10. <span data-ttu-id="390b9-180">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="390b9-180">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_003.png)
11. <span data-ttu-id="390b9-182">Copy the content of the downloaded certificate file, and then paste it into the **Signing certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="390b9-182">Copy the content of the downloaded certificate file, and then paste it into the **Signing certificate** textbox.</span></span>
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_004.png)
12. <span data-ttu-id="390b9-184">Confirm these URls match your configuration in step 3.</span><span class="sxs-lookup"><span data-stu-id="390b9-184">Confirm these URls match your configuration in step 3.</span></span>
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_005.png)
13. <span data-ttu-id="390b9-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="390b9-186">Click **Save** button.</span></span>
14. <span data-ttu-id="390b9-187">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-187">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]
15. <span data-ttu-id="390b9-189">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="390b9-189">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="390b9-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="390b9-191">Create an Azure AD test user</span></span>
<span data-ttu-id="390b9-192">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="390b9-192">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="390b9-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="390b9-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="390b9-195">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="390b9-195">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="390b9-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="390b9-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="390b9-198">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="390b9-198">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="390b9-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="390b9-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="390b9-202">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="390b9-202">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_05.png)
 1. <span data-ttu-id="390b9-204">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="390b9-204">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="390b9-205">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="390b9-205">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="390b9-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-206">Click **Next**.</span></span>
6. <span data-ttu-id="390b9-207">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="390b9-207">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="390b9-209">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="390b9-209">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="390b9-210">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="390b9-210">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="390b9-211">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="390b9-211">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="390b9-212">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="390b9-212">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="390b9-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="390b9-213">Click **Next**.</span></span>
7. <span data-ttu-id="390b9-214">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="390b9-214">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="390b9-216">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="390b9-216">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="390b9-218">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="390b9-218">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="390b9-219">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="390b9-219">Click **Complete**.</span></span>   

### <a name="create-a-front-test-user"></a><span data-ttu-id="390b9-220">Create a Front test user</span><span class="sxs-lookup"><span data-stu-id="390b9-220">Create a Front test user</span></span>
<span data-ttu-id="390b9-221">The objective of this section is to create a user called Britta Simon in Front.Please work with your Front support team to add the users in the Front account.</span><span class="sxs-lookup"><span data-stu-id="390b9-221">The objective of this section is to create a user called Britta Simon in Front.Please work with your Front support team to add the users in the Front account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="390b9-222">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="390b9-222">Assign the Azure AD test user</span></span>
<span data-ttu-id="390b9-223">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Front.</span><span class="sxs-lookup"><span data-stu-id="390b9-223">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Front.</span></span>

![Assign User][200]

<span data-ttu-id="390b9-225">**To assign Britta Simon to Front, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="390b9-225">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="390b9-226">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="390b9-226">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="390b9-228">In the applications list, select **Front**.</span><span class="sxs-lookup"><span data-stu-id="390b9-228">In the applications list, select **Front**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_50.png)
3. <span data-ttu-id="390b9-230">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="390b9-230">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="390b9-232">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="390b9-232">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="390b9-233">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="390b9-233">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="390b9-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="390b9-235">Test single sign-on</span></span>
<span data-ttu-id="390b9-236">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="390b9-236">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="390b9-237">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span><span class="sxs-lookup"><span data-stu-id="390b9-237">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="390b9-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="390b9-238">Additional resources</span></span>
* [<span data-ttu-id="390b9-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="390b9-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="390b9-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="390b9-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-front-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_205.png
































