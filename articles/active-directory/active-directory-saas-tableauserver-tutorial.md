---
title: 'Tutorial: Azure Active Directory integration with Tableau Server | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tableau Server.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 1d9aaef350057cacf7287e6a673cc670b3dcca6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553312"
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="19010-103">Tutorial: Azure Active Directory integration with Tableau Server</span><span class="sxs-lookup"><span data-stu-id="19010-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>
<span data-ttu-id="19010-104">The objective of this tutorial is to show you how to integrate Tableau Server with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19010-104">The objective of this tutorial is to show you how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19010-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="19010-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="19010-106">You can control in Azure AD who has access to Tableau Server</span><span class="sxs-lookup"><span data-stu-id="19010-106">You can control in Azure AD who has access to Tableau Server</span></span>
* <span data-ttu-id="19010-107">You can enable your users to automatically get signed-on to Tableau Server single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="19010-107">You can enable your users to automatically get signed-on to Tableau Server single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="19010-108">You can manage your accounts in one central location with the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="19010-108">You can manage your accounts in one central location with the Azure classic portal</span></span>

<span data-ttu-id="19010-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19010-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19010-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="19010-110">Prerequisites</span></span>
<span data-ttu-id="19010-111">To configure Azure AD integration with Tableau Server, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="19010-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

* <span data-ttu-id="19010-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="19010-112">An Azure AD subscription</span></span>
* <span data-ttu-id="19010-113">A Tableau Server SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="19010-113">A Tableau Server SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="19010-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="19010-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="19010-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="19010-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="19010-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="19010-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="19010-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19010-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19010-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="19010-118">Scenario Description</span></span>
<span data-ttu-id="19010-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="19010-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="19010-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="19010-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19010-121">Adding Tableau Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="19010-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="19010-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="19010-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-tableau-server-from-the-gallery"></a><span data-ttu-id="19010-123">Add Tableau Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="19010-123">Add Tableau Server from the gallery</span></span>
<span data-ttu-id="19010-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="19010-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19010-125">**To add Tableau Server from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19010-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19010-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19010-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="19010-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19010-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="19010-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19010-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="19010-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19010-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="19010-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="19010-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="19010-135">In the search box, type **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="19010-135">In the search box, type **Tableau Server**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_01.png)
7. <span data-ttu-id="19010-137">In the results pane, select **Tableau Server**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="19010-137">In the results pane, select **Tableau Server**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="19010-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="19010-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="19010-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19010-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19010-141">For SSO to work, Azure AD needs to know what the counterpart user in Tableau Server to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="19010-141">For SSO to work, Azure AD needs to know what the counterpart user in Tableau Server to an user in Azure AD is.</span></span> <span data-ttu-id="19010-142">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span><span class="sxs-lookup"><span data-stu-id="19010-142">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="19010-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="19010-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tableau Server.</span></span>

<span data-ttu-id="19010-144">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="19010-144">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19010-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="19010-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="19010-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19010-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19010-147">**[Creating a Tableau Server test user](#creating-a-tableauserver-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="19010-147">**[Creating a Tableau Server test user](#creating-a-tableauserver-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="19010-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="19010-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19010-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="19010-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="19010-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="19010-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="19010-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Tableau Server application.</span><span class="sxs-lookup"><span data-stu-id="19010-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Tableau Server application.</span></span>

<span data-ttu-id="19010-152">Tableau Server application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="19010-152">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="19010-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="19010-153">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_51.png) 

<span data-ttu-id="19010-155">**To configure Azure AD SSO with Tableau Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19010-155">**To configure Azure AD SSO with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="19010-156">In the Azure classic portal, on the **Tableau Server** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="19010-156">In the Azure classic portal, on the **Tableau Server** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_81.png) 
2. <span data-ttu-id="19010-158">On the **SAML token attributes** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19010-158">On the **SAML token attributes** dialog, perform the following steps:</span></span>

   1. <span data-ttu-id="19010-159">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="19010-159">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_82.png) 
   2. <span data-ttu-id="19010-161">In the **Attrubute Name** textbox, type **username**.</span><span class="sxs-lookup"><span data-stu-id="19010-161">In the **Attrubute Name** textbox, type **username**.</span></span>
   3. <span data-ttu-id="19010-162">From the **Attribute Value** list, selsect **user.displayname**.</span><span class="sxs-lookup"><span data-stu-id="19010-162">From the **Attribute Value** list, selsect **user.displayname**.</span></span>
   4. <span data-ttu-id="19010-163">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19010-163">Click **Complete**.</span></span>    

3. <span data-ttu-id="19010-164">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="19010-164">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_83.png)  
4. <span data-ttu-id="19010-166">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="19010-166">Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
5. <span data-ttu-id="19010-168">On the **How would you like users to sign on to Tableau Server** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-168">On the **How would you like users to sign on to Tableau Server** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_03.png) 
6. <span data-ttu-id="19010-170">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="19010-170">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_04.png) 

   1. <span data-ttu-id="19010-172">In the **Sign In URL** textbox, type the URL of your Tableau server.</span><span class="sxs-lookup"><span data-stu-id="19010-172">In the **Sign In URL** textbox, type the URL of your Tableau server.</span></span> 
   2. <span data-ttu-id="19010-173">In the **Identifier box** copy the URL.</span><span class="sxs-lookup"><span data-stu-id="19010-173">In the **Identifier box** copy the URL.</span></span>
   3. <span data-ttu-id="19010-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-174">Click **Next**.</span></span>

7. <span data-ttu-id="19010-175">On the **Configure single sign-on at Tableau Server** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="19010-175">On the **Configure single sign-on at Tableau Server** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_05.png) 

   1. <span data-ttu-id="19010-177">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="19010-177">Click **Download metadata**, and then save the file on your computer.</span></span>
   2. <span data-ttu-id="19010-178">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-178">Click **Next**.</span></span>

8. <span data-ttu-id="19010-179">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="19010-179">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   1. <span data-ttu-id="19010-180">In the Tableau Server configuration, click the **SAML** tab.</span><span class="sxs-lookup"><span data-stu-id="19010-180">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
   2. <span data-ttu-id="19010-182">Select the checkbox of **Use SAML for single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="19010-182">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   3. <span data-ttu-id="19010-183">Locate your Federation Metadata file downloaded from Azure classic portal, and then upload it in the **SAML Idp metadata file**.</span><span class="sxs-lookup"><span data-stu-id="19010-183">Locate your Federation Metadata file downloaded from Azure classic portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   4. <span data-ttu-id="19010-184">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="19010-184">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="19010-185">Using http://localhost is not recommended.</span><span class="sxs-lookup"><span data-stu-id="19010-185">Using http://localhost is not recommended.</span></span> <span data-ttu-id="19010-186">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span><span class="sxs-lookup"><span data-stu-id="19010-186">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="19010-187">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox as shown in the step 3</span><span class="sxs-lookup"><span data-stu-id="19010-187">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox as shown in the step 3</span></span>
   5. <span data-ttu-id="19010-188">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span><span class="sxs-lookup"><span data-stu-id="19010-188">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="19010-189">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span><span class="sxs-lookup"><span data-stu-id="19010-189">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="19010-190">Copy **SAML entity ID** and paste it to Azure AD **IDENTIFER** textbox as shown in the step 3.</span><span class="sxs-lookup"><span data-stu-id="19010-190">Copy **SAML entity ID** and paste it to Azure AD **IDENTIFER** textbox as shown in the step 3.</span></span>
   6. <span data-ttu-id="19010-191">Click on the **Export Metadata File** and open it in the text editor application.</span><span class="sxs-lookup"><span data-stu-id="19010-191">Click on the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="19010-192">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span><span class="sxs-lookup"><span data-stu-id="19010-192">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="19010-193">Now paste it to Azure AD **Reply URL** textbox as shown in step 3.</span><span class="sxs-lookup"><span data-stu-id="19010-193">Now paste it to Azure AD **Reply URL** textbox as shown in step 3.</span></span> 
   7. <span data-ttu-id="19010-194">Click the **OK** button in the Tableau Server Configiuration page.</span><span class="sxs-lookup"><span data-stu-id="19010-194">Click the **OK** button in the Tableau Server Configiuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="19010-195">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="19010-195">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >

9. <span data-ttu-id="19010-196">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-196">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="19010-198">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19010-198">On the **Single sign-on confirmation** page, click **Complete**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="19010-200">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19010-200">Create an Azure AD test user</span></span>
<span data-ttu-id="19010-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19010-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

* <span data-ttu-id="19010-202">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="19010-202">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="19010-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19010-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19010-205">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19010-205">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="19010-207">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="19010-207">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="19010-208">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="19010-208">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="19010-210">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="19010-210">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="19010-212">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19010-212">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="19010-214">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="19010-214">As **Type Of User**, select **New user in your organization**.</span></span>
   2. <span data-ttu-id="19010-215">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19010-215">In the **User Name** textbox, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="19010-216">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-216">Click **Next**.</span></span>
6. <span data-ttu-id="19010-217">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19010-217">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="19010-219">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="19010-219">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="19010-220">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="19010-220">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="19010-221">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="19010-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="19010-222">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="19010-222">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="19010-223">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="19010-223">Click **Next**.</span></span>
7. <span data-ttu-id="19010-224">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="19010-224">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="19010-226">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="19010-226">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="19010-228">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="19010-228">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="19010-229">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="19010-229">Click **Complete**.</span></span>   

### <a name="create-a-tableau-server-test-user"></a><span data-ttu-id="19010-230">Create a Tableau Server test user</span><span class="sxs-lookup"><span data-stu-id="19010-230">Create a Tableau Server test user</span></span>
<span data-ttu-id="19010-231">The objective of this section is to create a user called Britta Simon in Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="19010-231">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="19010-232">You need to provision all the users in the Tableau server.</span><span class="sxs-lookup"><span data-stu-id="19010-232">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="19010-233">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span><span class="sxs-lookup"><span data-stu-id="19010-233">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="19010-234">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="19010-234">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="19010-235">If you need to create an user manually, you need to contact the Tableau Server administrator in your organization.</span><span class="sxs-lookup"><span data-stu-id="19010-235">If you need to create an user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="19010-236">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="19010-236">Assign the Azure AD test user</span></span>
<span data-ttu-id="19010-237">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="19010-237">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Tableau Server.</span></span>

![Assign User][200] 

<span data-ttu-id="19010-239">**To assign Britta Simon to Tableau Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="19010-239">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="19010-240">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="19010-240">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="19010-242">In the applications list, select **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="19010-242">In the applications list, select **Tableau Server**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_50.png) 
3. <span data-ttu-id="19010-244">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="19010-244">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="19010-246">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="19010-246">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="19010-247">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="19010-247">In the toolbar on the bottom, click **Assign**.</span></span>

![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="19010-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="19010-249">Test single sign-on</span></span>
<span data-ttu-id="19010-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="19010-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="19010-251">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span><span class="sxs-lookup"><span data-stu-id="19010-251">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19010-252">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="19010-252">Additional Resources</span></span>
* [<span data-ttu-id="19010-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19010-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19010-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19010-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauserver-tutorial/tutorial_general_205.png






























