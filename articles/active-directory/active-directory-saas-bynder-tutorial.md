---
title: 'Tutorial: Azure Active Directory integration with Bynder | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bynder.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: cd174569bd18ed2f16566a7da666b6b4718bd8d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563357"
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="44131-103">Tutorial: Azure Active Directory integration with Bynder</span><span class="sxs-lookup"><span data-stu-id="44131-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="44131-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44131-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44131-105">Integrating Bynder with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="44131-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="44131-106">You can control in Azure AD who has access to Bynder</span><span class="sxs-lookup"><span data-stu-id="44131-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="44131-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="44131-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="44131-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="44131-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="44131-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44131-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44131-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="44131-110">Prerequisites</span></span>
<span data-ttu-id="44131-111">To configure Azure AD integration with Bynder, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="44131-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="44131-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="44131-112">An Azure AD subscription</span></span>
* <span data-ttu-id="44131-113">A Bynder single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="44131-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="44131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="44131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="44131-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="44131-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="44131-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="44131-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="44131-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44131-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44131-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="44131-118">Scenario description</span></span>
<span data-ttu-id="44131-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="44131-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="44131-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="44131-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44131-121">Adding Bynder from the gallery</span><span class="sxs-lookup"><span data-stu-id="44131-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="44131-122">Configuring and testing Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="44131-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="44131-123">Add Bynder from the gallery</span><span class="sxs-lookup"><span data-stu-id="44131-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="44131-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="44131-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44131-125">**To add Bynder from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44131-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44131-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44131-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="44131-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="44131-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="44131-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="44131-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="44131-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="44131-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="44131-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="44131-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="44131-135">In the search box, type **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="44131-135">In the search box, type **Bynder**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="44131-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="44131-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="44131-139">Configure and test Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="44131-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="44131-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="44131-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44131-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="44131-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="44131-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span><span class="sxs-lookup"><span data-stu-id="44131-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="44131-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span><span class="sxs-lookup"><span data-stu-id="44131-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="44131-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="44131-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44131-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="44131-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44131-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44131-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="44131-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="44131-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="44131-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="44131-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="44131-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="44131-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="44131-150">Configuring Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="44131-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="44131-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span><span class="sxs-lookup"><span data-stu-id="44131-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="44131-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44131-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="44131-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="44131-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="44131-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="44131-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="44131-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="44131-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="44131-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="44131-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-160">Click **Next**.</span></span>
4. <span data-ttu-id="44131-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="44131-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="44131-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="44131-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="44131-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span><span class="sxs-lookup"><span data-stu-id="44131-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="44131-166">To get the actual vlaue for your environment, contact Bynder.</span><span class="sxs-lookup"><span data-stu-id="44131-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="44131-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="44131-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="44131-169">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="44131-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="44131-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-170">Click **Next**.</span></span>
6. <span data-ttu-id="44131-171">To get SSO configured for your application, contact your Bynder support team.</span><span class="sxs-lookup"><span data-stu-id="44131-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="44131-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="44131-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="44131-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="44131-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="44131-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="44131-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="44131-177">Create an Azure AD test user</span></span>
<span data-ttu-id="44131-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44131-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="44131-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44131-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44131-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44131-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="44131-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="44131-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="44131-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="44131-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="44131-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="44131-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="44131-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44131-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="44131-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="44131-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="44131-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44131-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="44131-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-192">Click **Next**.</span></span>
6. <span data-ttu-id="44131-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44131-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="44131-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="44131-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="44131-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="44131-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="44131-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44131-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="44131-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="44131-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="44131-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="44131-199">Click **Next**.</span></span>
7. <span data-ttu-id="44131-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="44131-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="44131-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44131-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="44131-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="44131-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="44131-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="44131-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="44131-206">Create a Bynder test user</span><span class="sxs-lookup"><span data-stu-id="44131-206">Create a Bynder test user</span></span>
<span data-ttu-id="44131-207">The objective of this section is to create a user called Britta Simon in Bynder.</span><span class="sxs-lookup"><span data-stu-id="44131-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="44131-208">Bynder supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="44131-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="44131-209">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="44131-209">There is no action item for you in this section.</span></span> <span data-ttu-id="44131-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="44131-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="44131-211">If you need to create an user manually, you need to contact the Bynder support team.</span><span class="sxs-lookup"><span data-stu-id="44131-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="44131-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="44131-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="44131-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span><span class="sxs-lookup"><span data-stu-id="44131-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Assign User][200]

<span data-ttu-id="44131-215">**To assign Britta Simon to Bynder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44131-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="44131-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="44131-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="44131-218">In the applications list, select **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="44131-218">In the applications list, select **Bynder**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="44131-220">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="44131-220">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="44131-222">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44131-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="44131-223">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="44131-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="44131-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="44131-225">Test single sign-on</span></span>
<span data-ttu-id="44131-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="44131-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="44131-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span><span class="sxs-lookup"><span data-stu-id="44131-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44131-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="44131-228">Additional resources</span></span>
* [<span data-ttu-id="44131-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44131-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44131-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44131-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bynder-tutorial/tutorial_general_205.png


























