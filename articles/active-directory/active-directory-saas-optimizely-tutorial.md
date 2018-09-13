---
title: 'Tutorial: Azure Active Directory integration with Optimizely | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Optimizely.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: c762ba3a3dbd3b9d35b16a315cd084f1fd931b42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550940"
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="6c218-103">Tutorial: Azure Active Directory integration with Optimizely</span><span class="sxs-lookup"><span data-stu-id="6c218-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>
<span data-ttu-id="6c218-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c218-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c218-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6c218-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="6c218-106">You can control in Azure AD who has access to Optimizely</span><span class="sxs-lookup"><span data-stu-id="6c218-106">You can control in Azure AD who has access to Optimizely</span></span>
* <span data-ttu-id="6c218-107">You can enable your users to automatically get signed-on to Optimizely single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6c218-107">You can enable your users to automatically get signed-on to Optimizely single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="6c218-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="6c218-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="6c218-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c218-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c218-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c218-110">Prerequisites</span></span>
<span data-ttu-id="6c218-111">To configure Azure AD integration with Optimizely, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6c218-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

* <span data-ttu-id="6c218-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6c218-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6c218-113">A **Optimizely** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6c218-113">A **Optimizely** SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="6c218-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6c218-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 


<span data-ttu-id="6c218-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6c218-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6c218-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6c218-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6c218-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c218-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c218-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="6c218-118">Scenario Description</span></span>
<span data-ttu-id="6c218-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6c218-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="6c218-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c218-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c218-121">Adding Optimizely from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c218-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="6c218-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="6c218-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-optimizely-from-the-gallery"></a><span data-ttu-id="6c218-123">Add Optimizely from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c218-123">Add Optimizely from the gallery</span></span>
<span data-ttu-id="6c218-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6c218-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c218-125">**To add Optimizely from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c218-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c218-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c218-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="6c218-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6c218-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="6c218-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6c218-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="6c218-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6c218-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="6c218-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6c218-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="6c218-135">In the search box, type **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6c218-135">In the search box, type **Optimizely**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_01.png)

7. <span data-ttu-id="6c218-137">In the results pane, select **Optimizely**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6c218-137">In the results pane, select **Optimizely**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6c218-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c218-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6c218-140">In this section, you configure and test Azure AD SSO with Optimizely based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6c218-140">In this section, you configure and test Azure AD SSO with Optimizely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c218-141">For SSO to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c218-141">For SSO to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="6c218-142">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6c218-142">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="6c218-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="6c218-144">To configure and test Azure AD SSO with Optimizely, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c218-144">To configure and test Azure AD SSO with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c218-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6c218-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c218-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c218-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c218-147">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6c218-147">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6c218-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c218-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c218-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6c218-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6c218-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c218-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="6c218-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO  in your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="6c218-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO  in your Optimizely application.</span></span>

<span data-ttu-id="6c218-152">Optimizely application expects the SAML assertions to contain an attribute named "email".</span><span class="sxs-lookup"><span data-stu-id="6c218-152">Optimizely application expects the SAML assertions to contain an attribute named "email".</span></span> <span data-ttu-id="6c218-153">The value of "email" should be an Optimizely recognized email that can get authenticated by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c218-153">The value of "email" should be an Optimizely recognized email that can get authenticated by Azure AD.</span></span> <span data-ttu-id="6c218-154">Please configure the "email" claim for this application.</span><span class="sxs-lookup"><span data-stu-id="6c218-154">Please configure the "email" claim for this application.</span></span> 

<span data-ttu-id="6c218-155">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="6c218-155">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span></span> <span data-ttu-id="6c218-156">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="6c218-156">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_03.png) 

<span data-ttu-id="6c218-158">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c218-158">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6c218-159">In the Azure classic portal, on the **Optimizely** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="6c218-159">In the Azure classic portal, on the **Optimizely** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On][5]

2. <span data-ttu-id="6c218-161">On the SAML token attributes dialog, add the "email" attribute.</span><span class="sxs-lookup"><span data-stu-id="6c218-161">On the SAML token attributes dialog, add the "email" attribute.</span></span>
  1. <span data-ttu-id="6c218-162">Click **add user attribute** to open the **Add User Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c218-162">Click **add user attribute** to open the **Add User Attribute** dialog.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_05.png)
  2. <span data-ttu-id="6c218-164">In the **Attribute Name** textbox, type the attribute name "email".</span><span class="sxs-lookup"><span data-stu-id="6c218-164">In the **Attribute Name** textbox, type the attribute name "email".</span></span>
  3. <span data-ttu-id="6c218-165">From the **Attribute Value** list, select the attribute value "userprincipalname" or any value that contains an email recognized by Azure AD and Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-165">From the **Attribute Value** list, select the attribute value "userprincipalname" or any value that contains an email recognized by Azure AD and Optimizely.</span></span>
  4. <span data-ttu-id="6c218-166">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6c218-166">Click **Complete**.</span></span>

3. <span data-ttu-id="6c218-167">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="6c218-167">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]

4. <span data-ttu-id="6c218-169">In the classic portal, on the **Optimizely** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="6c218-169">In the classic portal, on the **Optimizely** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 

5. <span data-ttu-id="6c218-171">On the **How would you like users to sign on to Optimizely** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-171">On the **How would you like users to sign on to Optimizely** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_06.png)

6. <span data-ttu-id="6c218-173">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-173">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_07.png)
  1. <span data-ttu-id="6c218-175">In the **Sign On URL** textbox, type: `https://app.optimizely.net/contoso`</span><span class="sxs-lookup"><span data-stu-id="6c218-175">In the **Sign On URL** textbox, type: `https://app.optimizely.net/contoso`</span></span>
  2. <span data-ttu-id="6c218-176">In the **Identifier** textbox, type: `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="6c218-176">In the **Identifier** textbox, type: `urn:auth0:optimizely:contoso`</span></span>
  3. <span data-ttu-id="6c218-177">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-177">Click **Next**.</span></span> 

     >[!NOTE] 
     ><span data-ttu-id="6c218-178">The values for the **Sign On URL** and **Identifier** are only placeholders for the actual values.</span><span class="sxs-lookup"><span data-stu-id="6c218-178">The values for the **Sign On URL** and **Identifier** are only placeholders for the actual values.</span></span> <span data-ttu-id="6c218-179">You can find instructions for aquiring the actual values from Optimizely later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6c218-179">You can find instructions for aquiring the actual values from Optimizely later in this tutorial.</span></span>
     >

1. <span data-ttu-id="6c218-180">On the **Configure single sign-on at Optimizely** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-180">On the **Configure single sign-on at Optimizely** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_08.png)
 1. <span data-ttu-id="6c218-182">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6c218-182">Click **Download certificate**, and then save the file on your computer.</span></span>
 2. <span data-ttu-id="6c218-183">Copy the **Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="6c218-183">Copy the **Single Sign-On Service URL**.</span></span>

2. <span data-ttu-id="6c218-184">To get SSO configured for your application, contact your Optimizely Account Manager and provide the following information:</span><span class="sxs-lookup"><span data-stu-id="6c218-184">To get SSO configured for your application, contact your Optimizely Account Manager and provide the following information:</span></span>
   
  * <span data-ttu-id="6c218-185">Your downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="6c218-185">Your downloaded certificate</span></span> 
  * <span data-ttu-id="6c218-186">The single sign-on service URL</span><span class="sxs-lookup"><span data-stu-id="6c218-186">The single sign-on service URL</span></span>
     
  <span data-ttu-id="6c218-187">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span><span class="sxs-lookup"><span data-stu-id="6c218-187">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

3. <span data-ttu-id="6c218-188">Go back to **Configure App Settings** dialog page, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-188">Go back to **Configure App Settings** dialog page, and then perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_07.png) 
 1. <span data-ttu-id="6c218-190">In the **Sign On URL** textbox, type the **SP-initiated SSO URL** provided by Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-190">In the **Sign On URL** textbox, type the **SP-initiated SSO URL** provided by Optimizely.</span></span>  
 2. <span data-ttu-id="6c218-191">In the **Identifier** textbox, type the **Service Provider Entity ID** provided by Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-191">In the **Identifier** textbox, type the **Service Provider Entity ID** provided by Optimizely.</span></span>  
 3. <span data-ttu-id="6c218-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-192">Click **Next**.</span></span>

4. <span data-ttu-id="6c218-193">On the **Configure single sign-on at Optimizely** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-193">On the **Configure single sign-on at Optimizely** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][10] 
 1. <span data-ttu-id="6c218-195">Select the single sign-on configuration confirmation.</span><span class="sxs-lookup"><span data-stu-id="6c218-195">Select the single sign-on configuration confirmation.</span></span>  
 2. <span data-ttu-id="6c218-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-196">Click **Next**.</span></span>

5. <span data-ttu-id="6c218-197">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6c218-197">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

6. <span data-ttu-id="6c218-199">In a different browser window, sign-on to your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="6c218-199">In a different browser window, sign-on to your Optimizely application.</span></span>

7. <span data-ttu-id="6c218-200">Click you account name in the top right corner and then **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="6c218-200">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

8. <span data-ttu-id="6c218-202">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span><span class="sxs-lookup"><span data-stu-id="6c218-202">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6c218-204">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c218-204">Create an Azure AD test user</span></span>
<span data-ttu-id="6c218-205">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c218-205">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

* <span data-ttu-id="6c218-206">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6c218-206">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="6c218-208">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c218-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c218-209">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c218-209">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="6c218-211">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6c218-211">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="6c218-212">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6c218-212">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c218-214">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6c218-214">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="6c218-216">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-216">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="6c218-218">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="6c218-218">As Type Of User, select New user in your organization.</span></span> 
 2. <span data-ttu-id="6c218-219">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c218-219">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="6c218-220">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-220">Click **Next**.</span></span>

6. <span data-ttu-id="6c218-221">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-221">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="6c218-223">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6c218-223">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="6c218-224">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6c218-224">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="6c218-225">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6c218-225">In the **Display Name** textbox, type **Britta Simon**.</span></span>  
 4. <span data-ttu-id="6c218-226">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="6c218-226">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="6c218-227">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c218-227">Click **Next**.</span></span>

7. <span data-ttu-id="6c218-228">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="6c218-228">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="6c218-230">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c218-230">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="6c218-232">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="6c218-232">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="6c218-233">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6c218-233">Click **Complete**.</span></span>   

### <a name="create-an-optimizely-test-user"></a><span data-ttu-id="6c218-234">Create an Optimizely test user</span><span class="sxs-lookup"><span data-stu-id="6c218-234">Create an Optimizely test user</span></span>
<span data-ttu-id="6c218-235">In this section, you create a user called Britta Simon in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-235">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="6c218-236">On the home page, select **Collaborators** tab.</span><span class="sxs-lookup"><span data-stu-id="6c218-236">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="6c218-237">Click **New Collaborator** to add a new collaborator to the project.</span><span class="sxs-lookup"><span data-stu-id="6c218-237">Click **New Collaborator** to add a new collaborator to the project.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="6c218-239">Fill in the email address and assign them a role.</span><span class="sxs-lookup"><span data-stu-id="6c218-239">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="6c218-240">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="6c218-240">Click **Invite**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

1. <span data-ttu-id="6c218-242">They will receive an email invite.</span><span class="sxs-lookup"><span data-stu-id="6c218-242">They will receive an email invite.</span></span> <span data-ttu-id="6c218-243">Using the email address, they will have to log into Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-243">Using the email address, they will have to log into Optimizely.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6c218-244">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c218-244">Assign the Azure AD test user</span></span>
<span data-ttu-id="6c218-245">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6c218-245">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Optimizely.</span></span>

![Assign User][200] 

<span data-ttu-id="6c218-247">**To assign Britta Simon to Optimizely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c218-247">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6c218-248">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6c218-248">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="6c218-250">In the applications list, select **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6c218-250">In the applications list, select **Optimizely**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_50.png) 

3. <span data-ttu-id="6c218-252">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6c218-252">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="6c218-254">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6c218-254">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="6c218-255">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="6c218-255">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="6c218-257">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c218-257">Test single sign-on</span></span>
<span data-ttu-id="6c218-258">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6c218-258">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6c218-259">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="6c218-259">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c218-260">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="6c218-260">Additional Resources</span></span>
* [<span data-ttu-id="6c218-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c218-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c218-262">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c218-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-optimizely-tutorial/tutorial_general_205.png


































