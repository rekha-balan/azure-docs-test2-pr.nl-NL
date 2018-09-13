---
title: 'Tutorial: Azure Active Directory integration with vxMaintain | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and vxMaintain.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 23e7aab7d9a115d2826d85736bcd60abd6b11acc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661511"
---
# <a name="tutorial-azure-active-directory-integration-with-vxmaintain"></a><span data-ttu-id="1b6b6-103">Tutorial: Azure Active Directory integration with vxMaintain</span><span class="sxs-lookup"><span data-stu-id="1b6b6-103">Tutorial: Azure Active Directory integration with vxMaintain</span></span>
<span data-ttu-id="1b6b6-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b6b6-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b6b6-105">Integrating vxMaintain with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-105">Integrating vxMaintain with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1b6b6-106">You can control in Azure AD who has access to vxMaintain</span><span class="sxs-lookup"><span data-stu-id="1b6b6-106">You can control in Azure AD who has access to vxMaintain</span></span>
* <span data-ttu-id="1b6b6-107">You can enable your users to automatically get signed-on to vxMaintain single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1b6b6-107">You can enable your users to automatically get signed-on to vxMaintain single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1b6b6-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1b6b6-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1b6b6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b6b6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b6b6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b6b6-110">Prerequisites</span></span>
<span data-ttu-id="1b6b6-111">To configure Azure AD integration with vxMaintain, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-111">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

* <span data-ttu-id="1b6b6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1b6b6-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1b6b6-113">A vxMaintain single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1b6b6-113">A vxMaintain single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1b6b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1b6b6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1b6b6-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1b6b6-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b6b6-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b6b6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1b6b6-118">Scenario description</span></span>
<span data-ttu-id="1b6b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1b6b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b6b6-121">Adding vxMaintain from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b6b6-121">Adding vxMaintain from the gallery</span></span>
2. <span data-ttu-id="1b6b6-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1b6b6-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="1b6b6-123">Add vxMaintain from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b6b6-123">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="1b6b6-124">To configure the integration of vxMaintain into Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-124">To configure the integration of vxMaintain into Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b6b6-125">**To add vxMaintain from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-125">**To add vxMaintain from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6b6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="1b6b6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1b6b6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1b6b6-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1b6b6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1b6b6-135">In the search box, type **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-135">In the search box, type **vxMaintain**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_01.png)
7. <span data-ttu-id="1b6b6-137">In the results pane, select **vxMaintain**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-137">In the results pane, select **vxMaintain**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="1b6b6-138">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1b6b6-138">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="1b6b6-139">In this section, you configure and test Azure AD SSO with vxMaintain based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b6b6-139">In this section, you configure and test Azure AD SSO with vxMaintain based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b6b6-140">For SSO to work, Azure AD needs to know what the counterpart user in vxMaintain is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-140">For SSO to work, Azure AD needs to know what the counterpart user in vxMaintain is to a user in Azure AD.</span></span> <span data-ttu-id="1b6b6-141">In other words, a link relationship between an Azure AD user and the related user in vxMaintain needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-141">In other words, a link relationship between an Azure AD user and the related user in vxMaintain needs to be established.</span></span>

<span data-ttu-id="1b6b6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in vxMaintain.</span></span>

<span data-ttu-id="1b6b6-143">To configure and test Azure AD SSO with vxMaintain, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-143">To configure and test Azure AD SSO with vxMaintain, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b6b6-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b6b6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b6b6-146">**[Creating a vxMaintain test user](#creating-a-vxmaintain-test-user)** - to have a counterpart of Britta Simon in vxMaintain that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-146">**[Creating a vxMaintain test user](#creating-a-vxmaintain-test-user)** - to have a counterpart of Britta Simon in vxMaintain that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1b6b6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b6b6-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="1b6b6-149">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1b6b6-149">Configuring Azure AD SSO</span></span>
<span data-ttu-id="1b6b6-150">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your vxMaintain application.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-150">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your vxMaintain application.</span></span>

<span data-ttu-id="1b6b6-151">**To configure Azure AD single sign-on with vxMaintain, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-151">**To configure Azure AD single sign-on with vxMaintain, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6b6-152">In the classic portal, on the **vxMaintain** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-152">In the classic portal, on the **vxMaintain** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="1b6b6-154">On the **How would you like users to sign on to vxMaintain** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-154">On the **How would you like users to sign on to vxMaintain** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_03.png) 
3. <span data-ttu-id="1b6b6-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_04.png) 
  1. <span data-ttu-id="1b6b6-158">In the **Identifier URL** textbox, type the URL using the following pattern: **https://\<company name\>.verisae.com**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-158">In the **Identifier URL** textbox, type the URL using the following pattern: **https://\<company name\>.verisae.com**</span></span>
  2. <span data-ttu-id="1b6b6-159">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<company name\>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-159">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<company name\>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true**</span></span> 
  3. <span data-ttu-id="1b6b6-160">click **Next**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-160">click **Next**</span></span>
4. <span data-ttu-id="1b6b6-161">On the **Configure single sign-on at vxMaintain** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-161">On the **Configure single sign-on at vxMaintain** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_05.png)
  1. <span data-ttu-id="1b6b6-163">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-163">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="1b6b6-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-164">Click **Next**.</span></span>
5. <span data-ttu-id="1b6b6-165">To get SSO configured for your application, please reach out to Account Executive at Verisae and he will help you setup the SSO for your organization.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-165">To get SSO configured for your application, please reach out to Account Executive at Verisae and he will help you setup the SSO for your organization.</span></span> <span data-ttu-id="1b6b6-166">Provide them following information:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-166">Provide them following information:</span></span>
  * <span data-ttu-id="1b6b6-167">The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-167">The downloaded **metadata**</span></span>
6. <span data-ttu-id="1b6b6-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="1b6b6-170">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b6b6-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b6b6-172">Create an Azure AD test user</span></span>
<span data-ttu-id="1b6b6-173">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-173">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1b6b6-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6b6-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="1b6b6-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1b6b6-179">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-179">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="1b6b6-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="1b6b6-183">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-183">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

 ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1b6b6-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-185">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1b6b6-186">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1b6b6-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-187">Click **Next**.</span></span>
6. <span data-ttu-id="1b6b6-188">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-188">On the **User Profile** dialog page, perform the following steps:</span></span>

 ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_06.png)   
  1. <span data-ttu-id="1b6b6-190">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-190">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1b6b6-191">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-191">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1b6b6-192">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-192">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1b6b6-193">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-193">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="1b6b6-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-194">Click **Next**.</span></span>
7. <span data-ttu-id="1b6b6-195">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-195">On the **Get temporary password** dialog page, click **create**.</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="1b6b6-197">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b6b6-197">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/create_aaduser_08.png)   
  1. <span data-ttu-id="1b6b6-199">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-199">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="1b6b6-200">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-200">Click **Complete**.</span></span>   

### <a name="create-an-vxmaintain-test-user"></a><span data-ttu-id="1b6b6-201">Create an vxMaintain test user</span><span class="sxs-lookup"><span data-stu-id="1b6b6-201">Create an vxMaintain test user</span></span>
<span data-ttu-id="1b6b6-202">In this section, you create a user called Britta Simon in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-202">In this section, you create a user called Britta Simon in vxMaintain.</span></span> <span data-ttu-id="1b6b6-203">Please reach out to Account Executive at Verisae and he will help you to add the users in the vxMaintain platform.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-203">Please reach out to Account Executive at Verisae and he will help you to add the users in the vxMaintain platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1b6b6-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b6b6-204">Assign the Azure AD test user</span></span>
<span data-ttu-id="1b6b6-205">In this section, you enable Britta Simon to use Azure SSO by granting her access to vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-205">In this section, you enable Britta Simon to use Azure SSO by granting her access to vxMaintain.</span></span>

![Assign User][200] 

<span data-ttu-id="1b6b6-207">**To assign Britta Simon to vxMaintain, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b6b6-207">**To assign Britta Simon to vxMaintain, perform the following steps:**</span></span>

1. <span data-ttu-id="1b6b6-208">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-208">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="1b6b6-210">In the applications list, select **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-210">In the applications list, select **vxMaintain**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_50.png) 
3. <span data-ttu-id="1b6b6-212">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-212">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="1b6b6-214">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-214">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1b6b6-215">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-215">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1b6b6-217">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b6b6-217">Test single sign-on</span></span>
<span data-ttu-id="1b6b6-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1b6b6-219">When you click the vxMaintain tile in the Access Panel, you should get automatically signed-on to your vxMaintain application.</span><span class="sxs-lookup"><span data-stu-id="1b6b6-219">When you click the vxMaintain tile in the Access Panel, you should get automatically signed-on to your vxMaintain application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b6b6-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1b6b6-220">Additional resources</span></span>
* [<span data-ttu-id="1b6b6-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b6b6-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b6b6-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b6b6-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-vxmaintain-tutorial/tutorial_general_205.png
























