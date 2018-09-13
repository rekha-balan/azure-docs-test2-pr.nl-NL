---
title: 'Tutorial: Azure Active Directory integration with Voyance | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 14ead7edf6a333456565d6acd967ffc0849db2a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556289"
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="1e169-103">Tutorial: Azure Active Directory integration with Voyance</span><span class="sxs-lookup"><span data-stu-id="1e169-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="1e169-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e169-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e169-105">Integrating Voyance with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1e169-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e169-106">You can control in Azure AD who has access to Voyance</span><span class="sxs-lookup"><span data-stu-id="1e169-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="1e169-107">You can enable your users to automatically get signed-on to Voyance single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1e169-107">You can enable your users to automatically get signed-on to Voyance single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e169-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1e169-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1e169-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e169-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e169-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1e169-110">Prerequisites</span></span>

<span data-ttu-id="1e169-111">To configure Azure AD integration with Voyance, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1e169-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="1e169-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1e169-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e169-113">A Voyance SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1e169-113">A Voyance SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1e169-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1e169-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="1e169-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1e169-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e169-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1e169-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1e169-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e169-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1e169-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1e169-118">Scenario description</span></span>
<span data-ttu-id="1e169-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1e169-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e169-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1e169-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e169-121">Adding Voyance from the gallery</span><span class="sxs-lookup"><span data-stu-id="1e169-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="1e169-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1e169-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-voyance-from-the-gallery"></a><span data-ttu-id="1e169-123">Add Voyance from the gallery</span><span class="sxs-lookup"><span data-stu-id="1e169-123">Add Voyance from the gallery</span></span>
<span data-ttu-id="1e169-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1e169-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e169-125">**To add Voyance from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e169-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e169-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e169-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e169-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1e169-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1e169-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1e169-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="1e169-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1e169-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="1e169-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1e169-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="1e169-135">In the search box, type **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="1e169-135">In the search box, type **Voyance**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_01.png)

7. <span data-ttu-id="1e169-137">In the results pane, select **Voyance**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1e169-137">In the results pane, select **Voyance**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_0001.png)


## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1e169-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e169-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1e169-140">In this section, you configure and test Azure AD SSO with Voyance based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1e169-140">In this section, you configure and test Azure AD SSO with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e169-141">For SSO to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e169-141">For SSO to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="1e169-142">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1e169-142">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="1e169-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Voyance.</span><span class="sxs-lookup"><span data-stu-id="1e169-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Voyance.</span></span>

<span data-ttu-id="1e169-144">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1e169-144">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e169-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1e169-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e169-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e169-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e169-147">**[Creating a Voyance test user](#creating-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1e169-147">**[Creating a Voyance test user](#creating-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1e169-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e169-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e169-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1e169-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1e169-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e169-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1e169-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Voyance application.</span><span class="sxs-lookup"><span data-stu-id="1e169-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Voyance application.</span></span>


<span data-ttu-id="1e169-152">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e169-152">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="1e169-153">In the classic portal, on the **Voyance** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="1e169-153">In the classic portal, on the **Voyance** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>

    ![Configure Single Sign-On][6]

2. <span data-ttu-id="1e169-155">On the **How would you like users to sign on to Voyance** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-155">On the **How would you like users to sign on to Voyance** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_02.png)

3. <span data-ttu-id="1e169-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1e169-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_03.png)
  1. <span data-ttu-id="1e169-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com`.</span><span class="sxs-lookup"><span data-stu-id="1e169-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com`.</span></span>
  2. <span data-ttu-id="1e169-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com/saml/create/`.</span><span class="sxs-lookup"><span data-stu-id="1e169-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com/saml/create/`.</span></span>
  3. <span data-ttu-id="1e169-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-161">Click **Next**.</span></span>

4. <span data-ttu-id="1e169-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_04.png)
  1. <span data-ttu-id="1e169-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com/`.</span><span class="sxs-lookup"><span data-stu-id="1e169-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.nyansa.com/`.</span></span>
  2. <span data-ttu-id="1e169-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-165">Click **Next**.</span></span>

      >[!NOTE]
      ><span data-ttu-id="1e169-166">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="1e169-166">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="1e169-167">To get these values, contact [Voyance support team](emaiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="1e169-167">To get these values, contact [Voyance support team](emaiLto:support@nyansa.com).</span></span>
      >

5. <span data-ttu-id="1e169-168">On the **Configure single sign-on at Voyance** page, click **Download certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="1e169-168">On the **Configure single sign-on at Voyance** page, click **Download certificate** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_05.png) 

6. <span data-ttu-id="1e169-170">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1e169-170">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

7. <span data-ttu-id="1e169-171">Go to the top right corner of the navigation bar and click on the drop down that says "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="1e169-171">Go to the top right corner of the navigation bar and click on the drop down that says "**Acme University**".</span></span>
    
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

8. <span data-ttu-id="1e169-173">Click "**Admin Settings**".</span><span class="sxs-lookup"><span data-stu-id="1e169-173">Click "**Admin Settings**".</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

9. <span data-ttu-id="1e169-175">Click "**User Access**" tab.</span><span class="sxs-lookup"><span data-stu-id="1e169-175">Click "**User Access**" tab.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

10. <span data-ttu-id="1e169-177">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1e169-177">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

11. <span data-ttu-id="1e169-179">Go to **SAML v2** section and perform below steps:</span><span class="sxs-lookup"><span data-stu-id="1e169-179">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
 1. <span data-ttu-id="1e169-181">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="1e169-181">Select **Enabled**.</span></span>
 2. <span data-ttu-id="1e169-182">In the **IdP Login URL** textbox put the value of **SAML SSO URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="1e169-182">In the **IdP Login URL** textbox put the value of **SAML SSO URL** from Azure AD application configuration wizard.</span></span>
 3. <span data-ttu-id="1e169-183">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span><span class="sxs-lookup"><span data-stu-id="1e169-183">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
 4. <span data-ttu-id="1e169-184">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e169-184">Click **Save**.</span></span>

12. <span data-ttu-id="1e169-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

13. <span data-ttu-id="1e169-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1e169-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1e169-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1e169-189">Create an Azure AD test user</span></span>
<span data-ttu-id="1e169-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e169-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1e169-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e169-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e169-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e169-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="1e169-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1e169-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="1e169-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1e169-196">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e169-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1e169-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="1e169-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e169-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="1e169-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1e169-202">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="1e169-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e169-203">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="1e169-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-204">Click **Next**.</span></span>

6.  <span data-ttu-id="1e169-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e169-205">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="1e169-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1e169-207">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="1e169-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e169-208">In the **Last Name** textbox, type, **Simon**.</span></span>
 3. <span data-ttu-id="1e169-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e169-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
 4. <span data-ttu-id="1e169-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1e169-210">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="1e169-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e169-211">Click **Next**.</span></span>

7. <span data-ttu-id="1e169-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1e169-212">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="1e169-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1e169-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="1e169-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1e169-216">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="1e169-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1e169-217">Click **Complete**.</span></span>   

### <a name="create-a-voyance-test-user"></a><span data-ttu-id="1e169-218">Create a Voyance test user</span><span class="sxs-lookup"><span data-stu-id="1e169-218">Create a Voyance test user</span></span>

<span data-ttu-id="1e169-219">The objective of this section is to create a user called Britta Simon in Voyance.</span><span class="sxs-lookup"><span data-stu-id="1e169-219">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="1e169-220">Voyance supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1e169-220">Voyance supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1e169-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1e169-221">There is no action item for you in this section.</span></span> <span data-ttu-id="1e169-222">A new user will be created during an attempt to access Voyance if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="1e169-222">A new user will be created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1e169-223">If you need to create an user manually, you need to contact [Voyance support team](emaiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="1e169-223">If you need to create an user manually, you need to contact [Voyance support team](emaiLto:support@nyansa.com).</span></span>
>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1e169-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1e169-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="1e169-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Voyance.</span><span class="sxs-lookup"><span data-stu-id="1e169-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Voyance.</span></span>

![Assign User][200] 

<span data-ttu-id="1e169-227">**To assign Britta Simon to Voyance, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e169-227">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="1e169-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1e169-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="1e169-230">In the applications list, select **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="1e169-230">In the applications list, select **Voyance**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_voyance_50.png) 

3. <span data-ttu-id="1e169-232">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1e169-232">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="1e169-234">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e169-234">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="1e169-235">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1e169-235">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]


### <a name="test-single-sign-on"></a><span data-ttu-id="1e169-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1e169-237">Test single sign-on</span></span>

<span data-ttu-id="1e169-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1e169-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e169-239">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span><span class="sxs-lookup"><span data-stu-id="1e169-239">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1e169-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1e169-240">Additional resources</span></span>

* [<span data-ttu-id="1e169-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e169-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e169-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e169-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-voyance-tutorial/tutorial_general_205.png































