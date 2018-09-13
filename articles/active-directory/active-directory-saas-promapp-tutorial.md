---
title: 'Tutorial: Azure Active Directory integration with Promapp | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Promapp.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c998b96b7917a7ee5e2db229ed18f7711cde0dd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556689"
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="b4269-103">Tutorial: Azure Active Directory integration with Promapp</span><span class="sxs-lookup"><span data-stu-id="b4269-103">Tutorial: Azure Active Directory integration with Promapp</span></span>
<span data-ttu-id="b4269-104">The objective of this tutorial is to show you how to integrate Promapp with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4269-104">The objective of this tutorial is to show you how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4269-105">Integrating Promapp with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b4269-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="b4269-106">You can control in Azure AD who has access to Promapp</span><span class="sxs-lookup"><span data-stu-id="b4269-106">You can control in Azure AD who has access to Promapp</span></span> 
* <span data-ttu-id="b4269-107">You can enable your users to automatically get signed-on to Promapp single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b4269-107">You can enable your users to automatically get signed-on to Promapp single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="b4269-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="b4269-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="b4269-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4269-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4269-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4269-110">Prerequisites</span></span>
<span data-ttu-id="b4269-111">To configure Azure AD integration with Promapp, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b4269-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

* <span data-ttu-id="b4269-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b4269-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b4269-113">A Promapp single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b4269-113">A Promapp single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="b4269-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b4269-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="b4269-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b4269-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b4269-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b4269-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b4269-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4269-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="b4269-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="b4269-118">Scenario Description</span></span>
<span data-ttu-id="b4269-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b4269-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4269-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4269-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4269-121">Adding Promapp from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4269-121">Adding Promapp from the gallery</span></span> 
2. <span data-ttu-id="b4269-122">Configuring and testing Azure AD single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="b4269-122">Configuring and testing Azure AD single sign-on (SSO)</span></span>

## <a name="add-promapp-from-the-gallery"></a><span data-ttu-id="b4269-123">Add Promapp from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4269-123">Add Promapp from the gallery</span></span>
<span data-ttu-id="b4269-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b4269-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b4269-125">**To add Promapp from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4269-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b4269-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4269-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="b4269-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b4269-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b4269-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b4269-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="b4269-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b4269-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b4269-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b4269-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="b4269-135">In the search box, type **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="b4269-135">In the search box, type **Promapp**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="b4269-137">In the results pane, select **Promapp**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b4269-137">In the results pane, select **Promapp**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][500]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4269-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4269-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b4269-140">The objective of this section is to show you how to configure and test Azure AD SSO with Promapp based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4269-140">The objective of this section is to show you how to configure and test Azure AD SSO with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4269-141">For SSO to work, Azure AD needs to know what the counterpart user in Promapp to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="b4269-141">For SSO to work, Azure AD needs to know what the counterpart user in Promapp to an user in Azure AD is.</span></span> <span data-ttu-id="b4269-142">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b4269-142">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>  

<span data-ttu-id="b4269-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Promapp.</span><span class="sxs-lookup"><span data-stu-id="b4269-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Promapp.</span></span>

<span data-ttu-id="b4269-144">To configure and test Azure AD SSO with Promapp, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4269-144">To configure and test Azure AD SSO with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b4269-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b4269-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b4269-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4269-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4269-147">**[Creating a Promapp test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b4269-147">**[Creating a Promapp test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b4269-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b4269-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4269-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b4269-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4269-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4269-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="b4269-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your Promapp application.</span><span class="sxs-lookup"><span data-stu-id="b4269-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your Promapp application.</span></span>

<span data-ttu-id="b4269-152">**To configure Azure AD SSO with Promapp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4269-152">**To configure Azure AD SSO with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="b4269-153">In the Azure AD classic portal, on the **Promapp** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="b4269-153">In the Azure AD classic portal, on the **Promapp** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="b4269-155">On the **How would you like users to sign on to Promapp** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-155">On the **How would you like users to sign on to Promapp** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="b4269-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8] 
   
   1. <span data-ttu-id="b4269-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Promapp site (e.g.: *https://companyname.promapp.com/instancename*).</span><span class="sxs-lookup"><span data-stu-id="b4269-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Promapp site (e.g.: *https://companyname.promapp.com/instancename*).</span></span>
   2. <span data-ttu-id="b4269-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-160">Click **Next**.</span></span>

1. <span data-ttu-id="b4269-161">On the **Configure single sign-on at Promapp** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-161">On the **Configure single sign-on at Promapp** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9] 
   
   1. <span data-ttu-id="b4269-163">Click Download certificate, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b4269-163">Click Download certificate, and then save the file on your computer.</span></span>
   2. <span data-ttu-id="b4269-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-164">Click **Next**.</span></span>
   
2. <span data-ttu-id="b4269-165">Sign-on to your Promapp company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="b4269-165">Sign-on to your Promapp company site as administrator.</span></span> 
3. <span data-ttu-id="b4269-166">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b4269-166">In the menu on the top, click **Admin**.</span></span> 
   
    ![Azure AD Single Sign-On][12]
4. <span data-ttu-id="b4269-168">Click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="b4269-168">Click **Configure**.</span></span> 
   
    ![Azure AD Single Sign-On][13]
5. <span data-ttu-id="b4269-170">On the **Security** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-170">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][14] 
   
   1. <span data-ttu-id="b4269-172">In the Azure classic portal, on the **Configure single sign-on at Promapp** dialog, copy the **Remote Login URL**, paste it into the **SSO-Login URL** textbox, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b4269-172">In the Azure classic portal, on the **Configure single sign-on at Promapp** dialog, copy the **Remote Login URL**, paste it into the **SSO-Login URL** textbox, and then click **Save**.</span></span>
   2. <span data-ttu-id="b4269-173">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b4269-173">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>
   3. <span data-ttu-id="b4269-174">Open the downloaded certificate in notepad, copy the certificate content without the first line (*-----BEGIN CERTIFICATE-----*) and the last line (*-----END CERTIFICATE-----*), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b4269-174">Open the downloaded certificate in notepad, copy the certificate content without the first line (*-----BEGIN CERTIFICATE-----*) and the last line (*-----END CERTIFICATE-----*), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
6. <span data-ttu-id="b4269-175">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-175">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="b4269-177">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b4269-177">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4269-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4269-179">Create an Azure AD test user</span></span>
<span data-ttu-id="b4269-180">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4269-180">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b4269-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4269-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b4269-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4269-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="b4269-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b4269-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b4269-186">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b4269-186">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="b4269-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b4269-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="b4269-190">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-190">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_05.png)  
   
   1. <span data-ttu-id="b4269-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b4269-192">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="b4269-193">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4269-193">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="b4269-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-194">Click **Next**.</span></span>
   
6. <span data-ttu-id="b4269-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-195">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="b4269-197">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b4269-197">In the **First Name** textbox, type **Britta**.</span></span>   
   2. <span data-ttu-id="b4269-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4269-198">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="b4269-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4269-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="b4269-200">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b4269-200">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="b4269-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4269-201">Click **Next**.</span></span>
   
7. <span data-ttu-id="b4269-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b4269-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="b4269-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4269-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="b4269-206">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b4269-206">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="b4269-207">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b4269-207">Click **Complete**.</span></span>   

### <a name="create-a-promapp-test-user"></a><span data-ttu-id="b4269-208">Create a Promapp test user</span><span class="sxs-lookup"><span data-stu-id="b4269-208">Create a Promapp test user</span></span>
<span data-ttu-id="b4269-209">The Promapp application supports Just-in-Time provisioning.</span><span class="sxs-lookup"><span data-stu-id="b4269-209">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="b4269-210">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b4269-210">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b4269-211">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4269-211">Assign the Azure AD test user</span></span>
<span data-ttu-id="b4269-212">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Promapp.</span><span class="sxs-lookup"><span data-stu-id="b4269-212">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Promapp.</span></span>

![Assign User][200] 

<span data-ttu-id="b4269-214">**To assign Britta Simon to Promapp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4269-214">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="b4269-215">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b4269-215">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="b4269-217">In the applications list, select **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="b4269-217">In the applications list, select **Promapp**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="b4269-219">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b4269-219">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="b4269-221">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4269-221">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b4269-222">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b4269-222">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b4269-224">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4269-224">Test single sign-on</span></span>
<span data-ttu-id="b4269-225">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b4269-225">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b4269-226">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span><span class="sxs-lookup"><span data-stu-id="b4269-226">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4269-227">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="b4269-227">Additional Resources</span></span>
* [<span data-ttu-id="b4269-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4269-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4269-229">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4269-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_01.png

[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_500.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_02.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_promapp_10.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-promapp-tutorial/tutorial_general_205.png


[400]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_400.png
[401]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_401.png
[402]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_402.png




























