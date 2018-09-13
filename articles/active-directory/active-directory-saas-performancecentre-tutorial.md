---
title: 'Tutorial: Azure Active Directory integration with PerformanceCentre | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PerformanceCentre.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: db83d30cf5cef08832d0947f7adb6371e2a2267c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549801"
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="6a342-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="6a342-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>
<span data-ttu-id="6a342-104">The objective of this tutorial is to show you how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a342-104">The objective of this tutorial is to show you how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="6a342-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6a342-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="6a342-106">You can control in Azure AD who has access to PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="6a342-106">You can control in Azure AD who has access to PerformanceCentre</span></span> 
* <span data-ttu-id="6a342-107">You can enable your users to automatically get signed-on to PerformanceCentre single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6a342-107">You can enable your users to automatically get signed-on to PerformanceCentre single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="6a342-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="6a342-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="6a342-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a342-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a342-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a342-110">Prerequisites</span></span>
<span data-ttu-id="6a342-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6a342-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

* <span data-ttu-id="6a342-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6a342-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6a342-113">A PerformanceCentre single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6a342-113">A PerformanceCentre single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="6a342-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6a342-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="6a342-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6a342-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6a342-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6a342-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6a342-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a342-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="6a342-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="6a342-118">Scenario Description</span></span>
<span data-ttu-id="6a342-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6a342-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="6a342-120">The scenario outlined in this tutorial consists of these main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a342-120">The scenario outlined in this tutorial consists of these main building blocks:</span></span>

*  <span data-ttu-id="6a342-121">Adding PerformanceCentre from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a342-121">Adding PerformanceCentre from the gallery</span></span> 
*  <span data-ttu-id="6a342-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="6a342-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-performancecentre-from-the-gallery"></a><span data-ttu-id="6a342-123">Add PerformanceCentre from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a342-123">Add PerformanceCentre from the gallery</span></span>
<span data-ttu-id="6a342-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6a342-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a342-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a342-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a342-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a342-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="6a342-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6a342-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6a342-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6a342-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="6a342-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6a342-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="6a342-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6a342-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="6a342-135">In the search box, type **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="6a342-135">In the search box, type **PerformanceCentre**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="6a342-137">In the results pane, select **PerformanceCentre**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6a342-137">In the results pane, select **PerformanceCentre**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][500]

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="6a342-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="6a342-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="6a342-140">The objective of this section is to show you how to configure and test Azure AD SSO with PerformanceCentre based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6a342-140">The objective of this section is to show you how to configure and test Azure AD SSO with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a342-141">For SSO to work, Azure AD needs to know what the counterpart user in PerformanceCentre to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="6a342-141">For SSO to work, Azure AD needs to know what the counterpart user in PerformanceCentre to an user in Azure AD is.</span></span> <span data-ttu-id="6a342-142">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6a342-142">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>  

<span data-ttu-id="6a342-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="6a342-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PerformanceCentre.</span></span>

<span data-ttu-id="6a342-144">**To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:**</span><span class="sxs-lookup"><span data-stu-id="6a342-144">**To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:**</span></span>

1. <span data-ttu-id="6a342-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6a342-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a342-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a342-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a342-147">**[Creating a PerformanceCentre test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6a342-147">**[Creating a PerformanceCentre test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6a342-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a342-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a342-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6a342-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6a342-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a342-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="6a342-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your PerformanceCentre application.</span><span class="sxs-lookup"><span data-stu-id="6a342-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your PerformanceCentre application.</span></span>

<span data-ttu-id="6a342-152">**To configure Azure AD SSO with PerformanceCentre, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a342-152">**To configure Azure AD SSO with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="6a342-153">In the Azure AD classic portal, on the **PerformanceCentre** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="6a342-153">In the Azure AD classic portal, on the **PerformanceCentre** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="6a342-155">On the **How would you like users to sign on to PerformanceCentre** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a342-155">On the **How would you like users to sign on to PerformanceCentre** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="6a342-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8] 
   
   1. <span data-ttu-id="6a342-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your PerformanceCentre site (e.g.: *http://companyname.performancecentre.com/saml/SSO*).</span><span class="sxs-lookup"><span data-stu-id="6a342-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your PerformanceCentre site (e.g.: *http://companyname.performancecentre.com/saml/SSO*).</span></span>
   2. <span data-ttu-id="6a342-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a342-160">Click **Next**.</span></span>
4. <span data-ttu-id="6a342-161">On the **Configure single sign-on at PerformanceCentre** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-161">On the **Configure single sign-on at PerformanceCentre** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9] 
   
  * <span data-ttu-id="6a342-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6a342-163">Click **Download metadata**, and then save the file on your computer.</span></span>
5. <span data-ttu-id="6a342-164">Sign-on to your **PerformanceCentre** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="6a342-164">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>
6. <span data-ttu-id="6a342-165">In the tab on the left side, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="6a342-165">In the tab on the left side, click **Configure**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="6a342-167">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="6a342-167">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD Single Sign-On][11]
8. <span data-ttu-id="6a342-169">As **Protocol**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6a342-169">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD Single Sign-On][12]
9. <span data-ttu-id="6a342-171">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a342-171">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD Single Sign-On][13]
10. <span data-ttu-id="6a342-173">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span><span class="sxs-lookup"><span data-stu-id="6a342-173">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD Single Sign-On][14]
11. <span data-ttu-id="6a342-175">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a342-175">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
    
     ![Azure AD Single Sign-On][15]
12. <span data-ttu-id="6a342-177">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6a342-177">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][16]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a342-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a342-179">Create an Azure AD test user</span></span>
<span data-ttu-id="6a342-180">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a342-180">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="6a342-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a342-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a342-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a342-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="6a342-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6a342-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6a342-186">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6a342-186">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="6a342-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6a342-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="6a342-190">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-190">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_05.png)  
   
   1. <span data-ttu-id="6a342-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="6a342-192">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="6a342-193">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a342-193">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="6a342-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a342-194">Click **Next**.</span></span>
   
6. <span data-ttu-id="6a342-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-195">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="6a342-197">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6a342-197">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="6a342-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a342-198">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="6a342-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a342-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="6a342-200">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="6a342-200">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="6a342-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a342-201">Click **Next**.</span></span>
   
7. <span data-ttu-id="6a342-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="6a342-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="6a342-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="6a342-206">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="6a342-206">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="6a342-207">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6a342-207">Click **Complete**.</span></span>   

### <a name="create-a-performancecentre-test-user"></a><span data-ttu-id="6a342-208">Create a PerformanceCentre test user</span><span class="sxs-lookup"><span data-stu-id="6a342-208">Create a PerformanceCentre test user</span></span>
<span data-ttu-id="6a342-209">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="6a342-209">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="6a342-210">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a342-210">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="6a342-211">Sign on to your PerformanceCentre company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="6a342-211">Sign on to your PerformanceCentre company site as administrator.</span></span>
2. <span data-ttu-id="6a342-212">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span><span class="sxs-lookup"><span data-stu-id="6a342-212">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Create User][400]
3. <span data-ttu-id="6a342-214">On the **Interrelate - Create Participant** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a342-214">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Create User][401]
   
   1. <span data-ttu-id="6a342-216">Type the required attributes for Britta Simon into related textboxes.</span><span class="sxs-lookup"><span data-stu-id="6a342-216">Type the required attributes for Britta Simon into related textboxes.</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="6a342-217">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a342-217">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    > 
    > 
 
   2. <span data-ttu-id="6a342-218">Select **Client Administrator** as **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="6a342-218">Select **Client Administrator** as **Choose Role**.</span></span>
   3. <span data-ttu-id="6a342-219">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a342-219">Click **Save**.</span></span>   


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6a342-220">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a342-220">Assign the Azure AD test user</span></span>
<span data-ttu-id="6a342-221">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="6a342-221">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to PerformanceCentre.</span></span>

![Assign User][200] 

<span data-ttu-id="6a342-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a342-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="6a342-224">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6a342-224">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="6a342-226">In the applications list, select **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="6a342-226">In the applications list, select **PerformanceCentre**.</span></span>
   
    ![Assign User][202]
3. <span data-ttu-id="6a342-228">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6a342-228">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="6a342-230">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a342-230">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6a342-231">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="6a342-231">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="6a342-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a342-233">Test single sign-on</span></span>
<span data-ttu-id="6a342-234">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6a342-234">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="6a342-235">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span><span class="sxs-lookup"><span data-stu-id="6a342-235">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a342-236">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="6a342-236">Additional Resources</span></span>
* [<span data-ttu-id="6a342-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a342-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a342-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a342-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_01.png
[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_06.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_07.png


[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_50.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_205.png


[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png
[402]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_402.png



































