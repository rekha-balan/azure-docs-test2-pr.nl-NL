---
title: 'Tutorial: Azure Active Directory integration with ICIMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ICIMS.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: e0d91533f28c2f46aee7b60fa15be684b0d18de6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553156"
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="ab663-103">Tutorial: Azure Active Directory integration with ICIMS</span><span class="sxs-lookup"><span data-stu-id="ab663-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>
<span data-ttu-id="ab663-104">The objective of this tutorial is to show you how to integrate ICIMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab663-104">The objective of this tutorial is to show you how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab663-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ab663-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ab663-106">You can control in Azure AD who has access to ICIMS</span><span class="sxs-lookup"><span data-stu-id="ab663-106">You can control in Azure AD who has access to ICIMS</span></span>
* <span data-ttu-id="ab663-107">You can enable your users to automatically get signed-on to ICIMS single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ab663-107">You can enable your users to automatically get signed-on to ICIMS single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ab663-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ab663-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ab663-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab663-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab663-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab663-110">Prerequisites</span></span>
<span data-ttu-id="ab663-111">To configure Azure AD integration with ICIMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ab663-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

* <span data-ttu-id="ab663-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ab663-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ab663-113">A ICIMS single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ab663-113">A ICIMS single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ab663-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ab663-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 

<span data-ttu-id="ab663-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ab663-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ab663-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ab663-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ab663-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab663-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab663-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ab663-118">Scenario Description</span></span>
<span data-ttu-id="ab663-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ab663-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="ab663-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ab663-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab663-121">Adding ICIMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="ab663-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="ab663-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ab663-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-icims-from-the-gallery"></a><span data-ttu-id="ab663-123">Add ICIMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="ab663-123">Add ICIMS from the gallery</span></span>
<span data-ttu-id="ab663-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ab663-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab663-125">**To add ICIMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ab663-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab663-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab663-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ab663-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ab663-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ab663-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ab663-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ab663-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ab663-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ab663-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ab663-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ab663-135">In the search box, type **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="ab663-135">In the search box, type **ICIMS**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_01.png)
7. <span data-ttu-id="ab663-137">In the results pane, select **ICIMS**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ab663-137">In the results pane, select **ICIMS**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="ab663-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ab663-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="ab663-140">The objective of this section is to show you how to configure and test Azure AD SSO with ICIMS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ab663-140">The objective of this section is to show you how to configure and test Azure AD SSO with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab663-141">For SSO to work, Azure AD needs to know what the counterpart user in ICIMS to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ab663-141">For SSO to work, Azure AD needs to know what the counterpart user in ICIMS to an user in Azure AD is.</span></span> <span data-ttu-id="ab663-142">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ab663-142">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>  

<span data-ttu-id="ab663-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ICIMS.</span><span class="sxs-lookup"><span data-stu-id="ab663-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ICIMS.</span></span>

<span data-ttu-id="ab663-144">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ab663-144">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab663-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ab663-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab663-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab663-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab663-147">**[Creating a ICIMS test user](#creating-a-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ab663-147">**[Creating a ICIMS test user](#creating-a-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ab663-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ab663-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab663-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ab663-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ab663-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ab663-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="ab663-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your ICIMS application.</span><span class="sxs-lookup"><span data-stu-id="ab663-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your ICIMS application.</span></span>

<span data-ttu-id="ab663-152">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ab663-152">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ab663-153">In the Azure classic portal, on the **ICIMS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="ab663-153">In the Azure classic portal, on the **ICIMS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="ab663-155">On the **How would you like users to sign on to ICIMS** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-155">On the **How would you like users to sign on to ICIMS** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_03.png) 
3. <span data-ttu-id="ab663-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab663-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_04.png) 
  1. <span data-ttu-id="ab663-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your ICIMS application using the following pattern: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="ab663-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your ICIMS application using the following pattern: `https://<tenant name>.icims.com`</span></span>
  2. <span data-ttu-id="ab663-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-160">Click **Next**.</span></span>
4. <span data-ttu-id="ab663-161">On the **Configure single sign-on at ICIMS** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab663-161">On the **Configure single sign-on at ICIMS** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_05.png)   
  1. <span data-ttu-id="ab663-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ab663-163">Click **Download metadata**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="ab663-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-164">Click **Next**.</span></span>
5. <span data-ttu-id="ab663-165">To get SSO configured for your application, contact your ICIMS support team and email the attach downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="ab663-165">To get SSO configured for your application, contact your ICIMS support team and email the attach downloaded metadata file.</span></span> <span data-ttu-id="ab663-166">Also please do provide the Issuer URL, SAML SSO URL and Sign Out URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="ab663-166">Also please do provide the Issuer URL, SAML SSO URL and Sign Out URL so that they can be configured for SSO integration.</span></span>
6. <span data-ttu-id="ab663-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="ab663-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ab663-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab663-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ab663-171">Create an Azure AD test user</span></span>
<span data-ttu-id="ab663-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab663-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

 * <span data-ttu-id="ab663-173">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ab663-173">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="ab663-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ab663-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab663-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab663-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="ab663-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ab663-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ab663-179">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ab663-179">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="ab663-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ab663-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="ab663-183">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab663-183">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="ab663-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="ab663-185">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="ab663-186">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab663-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ab663-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-187">Click **Next**.</span></span>
6. <span data-ttu-id="ab663-188">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab663-188">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_06.png)  
  1. <span data-ttu-id="ab663-190">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ab663-190">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="ab663-191">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ab663-191">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="ab663-192">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ab663-192">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ab663-193">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ab663-193">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ab663-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ab663-194">Click **Next**.</span></span>
7. <span data-ttu-id="ab663-195">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ab663-195">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="ab663-197">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab663-197">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/create_aaduser_08.png)  
  1. <span data-ttu-id="ab663-199">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ab663-199">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="ab663-200">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ab663-200">Click **Complete**.</span></span>   

### <a name="create-a-icims-test-user"></a><span data-ttu-id="ab663-201">Create a ICIMS test user</span><span class="sxs-lookup"><span data-stu-id="ab663-201">Create a ICIMS test user</span></span>
<span data-ttu-id="ab663-202">The objective of this section is to create a user called Britta Simon in ICIMS.</span><span class="sxs-lookup"><span data-stu-id="ab663-202">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="ab663-203">Please work with ICIMS support team to add the users in the ICIMS account.</span><span class="sxs-lookup"><span data-stu-id="ab663-203">Please work with ICIMS support team to add the users in the ICIMS account.</span></span> 

>[!NOTE]
><span data-ttu-id="ab663-204">If you need to create an user manually, you need to contact the ICIMS support team.</span><span class="sxs-lookup"><span data-stu-id="ab663-204">If you need to create an user manually, you need to contact the ICIMS support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ab663-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ab663-205">Assign the Azure AD test user</span></span>
<span data-ttu-id="ab663-206">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ICIMS.</span><span class="sxs-lookup"><span data-stu-id="ab663-206">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ICIMS.</span></span>

![Assign User][200] 

<span data-ttu-id="ab663-208">**To assign Britta Simon to ICIMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ab663-208">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ab663-209">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ab663-209">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="ab663-211">In the applications list, select **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="ab663-211">In the applications list, select **ICIMS**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_icims_50.png) 
3. <span data-ttu-id="ab663-213">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ab663-213">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="ab663-215">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ab663-215">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ab663-216">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ab663-216">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ab663-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ab663-218">Test single sign-on</span></span>
<span data-ttu-id="ab663-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ab663-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="ab663-220">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span><span class="sxs-lookup"><span data-stu-id="ab663-220">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab663-221">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ab663-221">Additional Resources</span></span>
* [<span data-ttu-id="ab663-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab663-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab663-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab663-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-icims-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-icims-tutorial/tutorial_general_205.png

























