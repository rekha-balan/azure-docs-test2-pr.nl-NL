---
title: 'Tutorial: Azure Active Directory integration with Allocadia | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Allocadia.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 2dd6e1802084d79201031f25e255c4ab33a8b2c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553155"
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="5df63-103">Tutorial: Azure Active Directory integration with Allocadia</span><span class="sxs-lookup"><span data-stu-id="5df63-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>
<span data-ttu-id="5df63-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5df63-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5df63-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5df63-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5df63-106">You can control in Azure AD who has access to Allocadia</span><span class="sxs-lookup"><span data-stu-id="5df63-106">You can control in Azure AD who has access to Allocadia</span></span>
* <span data-ttu-id="5df63-107">You can enable your users to automatically sign in to Allocadia using single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5df63-107">You can enable your users to automatically sign in to Allocadia using single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="5df63-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="5df63-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5df63-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5df63-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5df63-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5df63-110">Prerequisites</span></span>
<span data-ttu-id="5df63-111">To configure Azure AD integration with Allocadia, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5df63-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

* <span data-ttu-id="5df63-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5df63-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5df63-113">A Allocadia SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5df63-113">A Allocadia SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="5df63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5df63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="5df63-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5df63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5df63-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5df63-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5df63-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5df63-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5df63-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="5df63-118">Scenario Description</span></span>
<span data-ttu-id="5df63-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5df63-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="5df63-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5df63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5df63-121">Adding Allocadia from the gallery</span><span class="sxs-lookup"><span data-stu-id="5df63-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="5df63-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="5df63-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-allocadia-from-the-gallery"></a><span data-ttu-id="5df63-123">Add Allocadia from the gallery</span><span class="sxs-lookup"><span data-stu-id="5df63-123">Add Allocadia from the gallery</span></span>
<span data-ttu-id="5df63-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5df63-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5df63-125">**To add Allocadia from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5df63-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5df63-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5df63-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="5df63-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5df63-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5df63-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5df63-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="5df63-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5df63-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="5df63-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5df63-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="5df63-135">In the search box, type **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="5df63-135">In the search box, type **Allocadia**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_01.png)

7. <span data-ttu-id="5df63-137">In the results pane, select **Allocadia**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5df63-137">In the results pane, select **Allocadia**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5df63-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5df63-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5df63-140">In this section, you configure and test Azure AD SSO with Allocadia based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5df63-140">In this section, you configure and test Azure AD SSO with Allocadia based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5df63-141">For SSO to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5df63-141">For SSO to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="5df63-142">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5df63-142">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="5df63-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Allocadia.</span><span class="sxs-lookup"><span data-stu-id="5df63-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Allocadia.</span></span>

<span data-ttu-id="5df63-144">To configure and test Azure AD SSO with Allocadia, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5df63-144">To configure and test Azure AD SSO with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5df63-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5df63-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5df63-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5df63-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5df63-147">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5df63-147">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5df63-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5df63-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5df63-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5df63-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5df63-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5df63-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="5df63-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Allocadia application.</span><span class="sxs-lookup"><span data-stu-id="5df63-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Allocadia application.</span></span>

<span data-ttu-id="5df63-152">Allocadia application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="5df63-152">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5df63-153">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="5df63-153">Please configure the following claims for this application.</span></span> <span data-ttu-id="5df63-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="5df63-154">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="5df63-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="5df63-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_07.png) 

<span data-ttu-id="5df63-157">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5df63-157">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="5df63-158">In the Azure classic portal, on the **Allocadia** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="5df63-158">In the Azure classic portal, on the **Allocadia** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_80.png) 

2. <span data-ttu-id="5df63-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5df63-160">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
   
    | <span data-ttu-id="5df63-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="5df63-161">Attribute Name</span></span> | <span data-ttu-id="5df63-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="5df63-162">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5df63-163">firstname</span><span class="sxs-lookup"><span data-stu-id="5df63-163">firstname</span></span> |<span data-ttu-id="5df63-164">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5df63-164">user.givenname</span></span> |
    | <span data-ttu-id="5df63-165">lastname</span><span class="sxs-lookup"><span data-stu-id="5df63-165">lastname</span></span> |<span data-ttu-id="5df63-166">user.surname</span><span class="sxs-lookup"><span data-stu-id="5df63-166">user.surname</span></span> |
    | <span data-ttu-id="5df63-167">email</span><span class="sxs-lookup"><span data-stu-id="5df63-167">email</span></span> |<span data-ttu-id="5df63-168">user.mail</span><span class="sxs-lookup"><span data-stu-id="5df63-168">user.mail</span></span> |

  1. <span data-ttu-id="5df63-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="5df63-169">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_81.png) 
  2. <span data-ttu-id="5df63-171">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5df63-171">In the **Attrubute Name** textbox, type the attribute name shown for that row.</span></span>
  3. <span data-ttu-id="5df63-172">From the **Attribute Value** list, selsect the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="5df63-172">From the **Attribute Value** list, selsect the attribute value shown for that row.</span></span>
  4. <span data-ttu-id="5df63-173">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5df63-173">Click **Complete**.</span></span>    
 
3. <span data-ttu-id="5df63-174">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="5df63-174">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_83.png)  

4. <span data-ttu-id="5df63-176">On the **How would you like users to sign on to Allocadia** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5df63-176">On the **How would you like users to sign on to Allocadia** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_03.png) 

5. <span data-ttu-id="5df63-178">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="5df63-178">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_04.png)  
  1. <span data-ttu-id="5df63-180">In the IDENTIFER box type the URL in the following pattern: For test environment use the URL as **"https://na2standby.allocadia.com"** and for production environment use **"https://na2.allocadia.com"**.</span><span class="sxs-lookup"><span data-stu-id="5df63-180">In the IDENTIFER box type the URL in the following pattern: For test environment use the URL as **"https://na2standby.allocadia.com"** and for production environment use **"https://na2.allocadia.com"**.</span></span>
  2. <span data-ttu-id="5df63-181">In the Reply URL type the URL in the following pattern: For test environment use the URL pattern as  **"https://na2standby.allocadia.com/allocadia/saml/SSO"** and for production environment use **"https://na2.allocadia.com/allocadia/saml/SSO"**</span><span class="sxs-lookup"><span data-stu-id="5df63-181">In the Reply URL type the URL in the following pattern: For test environment use the URL pattern as  **"https://na2standby.allocadia.com/allocadia/saml/SSO"** and for production environment use **"https://na2.allocadia.com/allocadia/saml/SSO"**</span></span>

6. <span data-ttu-id="5df63-182">On the **Configure single sign-on at Allocadia** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5df63-182">On the **Configure single sign-on at Allocadia** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_05.png) 
  1. <span data-ttu-id="5df63-184">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5df63-184">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="5df63-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5df63-185">Click **Next**.</span></span>

7. <span data-ttu-id="5df63-186">To get SSO configured for your application, contact [Allocadia Support](mailTo:support@allocadia.com) team and they will assist to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="5df63-186">To get SSO configured for your application, contact [Allocadia Support](mailTo:support@allocadia.com) team and they will assist to configure SSO.</span></span> <span data-ttu-id="5df63-187">Please note that you have to send email and attach downloaded metadata file to configure SSO on the Allocadia side.</span><span class="sxs-lookup"><span data-stu-id="5df63-187">Please note that you have to send email and attach downloaded metadata file to configure SSO on the Allocadia side.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5df63-188">Please make sure that Allocadia team set the Identifier value in the test environment as **"https://na2standby.allocadia.com"** and for production environment, it should be: **"https://na2.allocadia.com"**</span><span class="sxs-lookup"><span data-stu-id="5df63-188">Please make sure that Allocadia team set the Identifier value in the test environment as **"https://na2standby.allocadia.com"** and for production environment, it should be: **"https://na2.allocadia.com"**</span></span>
   >  

8. <span data-ttu-id="5df63-189">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5df63-189">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

9. <span data-ttu-id="5df63-191">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5df63-191">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5df63-193">CreatE an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5df63-193">CreatE an Azure AD test user</span></span>
<span data-ttu-id="5df63-194">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5df63-194">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

* <span data-ttu-id="5df63-195">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5df63-195">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="5df63-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5df63-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5df63-198">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5df63-198">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="5df63-200">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="5df63-200">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5df63-201">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5df63-201">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5df63-203">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="5df63-203">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="5df63-205">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5df63-205">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="5df63-207">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="5df63-207">As Type Of User, select New user in your organization.</span></span>   
 2. <span data-ttu-id="5df63-208">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5df63-208">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="5df63-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5df63-209">Click **Next**.</span></span>

6. <span data-ttu-id="5df63-210">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5df63-210">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="5df63-212">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5df63-212">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="5df63-213">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5df63-213">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="5df63-214">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5df63-214">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="5df63-215">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="5df63-215">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="5df63-216">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5df63-216">Click **Next**.</span></span>

7. <span data-ttu-id="5df63-217">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="5df63-217">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="5df63-219">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5df63-219">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="5df63-221">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="5df63-221">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="5df63-222">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5df63-222">Click **Complete**.</span></span>   

### <a name="create-an-allocadia-test-user"></a><span data-ttu-id="5df63-223">CreatE an Allocadia test user</span><span class="sxs-lookup"><span data-stu-id="5df63-223">CreatE an Allocadia test user</span></span>
<span data-ttu-id="5df63-224">In this section, you create a user called Britta Simon in Allocadia.</span><span class="sxs-lookup"><span data-stu-id="5df63-224">In this section, you create a user called Britta Simon in Allocadia.</span></span> <span data-ttu-id="5df63-225">Allocadia application support just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="5df63-225">Allocadia application support just in time user provisioning.</span></span> <span data-ttu-id="5df63-226">If you have configured the claims as stated above in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** section then it will provision the users in the application.</span><span class="sxs-lookup"><span data-stu-id="5df63-226">If you have configured the claims as stated above in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** section then it will provision the users in the application.</span></span> 

>[!NOTE]
><span data-ttu-id="5df63-227">If you need to create a user manually or batch of users, you need to contact the Allocadia support team.</span><span class="sxs-lookup"><span data-stu-id="5df63-227">If you need to create a user manually or batch of users, you need to contact the Allocadia support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5df63-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5df63-228">Assign the Azure AD test user</span></span>
<span data-ttu-id="5df63-229">In this section, you enable Britta Simon to use Azure sso by granting her access to Allocadia.</span><span class="sxs-lookup"><span data-stu-id="5df63-229">In this section, you enable Britta Simon to use Azure sso by granting her access to Allocadia.</span></span>

![Assign User][200] 

<span data-ttu-id="5df63-231">**To assign Britta Simon to Allocadia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5df63-231">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="5df63-232">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5df63-232">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="5df63-234">In the applications list, select **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="5df63-234">In the applications list, select **Allocadia**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_50.png) 

3. <span data-ttu-id="5df63-236">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5df63-236">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="5df63-238">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5df63-238">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="5df63-239">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="5df63-239">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="5df63-241">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5df63-241">Test Single Sign-On</span></span>
<span data-ttu-id="5df63-242">In this section, you test your Azure AD sso configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5df63-242">In this section, you test your Azure AD sso configuration using the Access Panel.</span></span>

<span data-ttu-id="5df63-243">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span><span class="sxs-lookup"><span data-stu-id="5df63-243">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5df63-244">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="5df63-244">Additional Resources</span></span>
* [<span data-ttu-id="5df63-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5df63-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5df63-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5df63-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-allocadia-tutorial/tutorial_general_205.png





























