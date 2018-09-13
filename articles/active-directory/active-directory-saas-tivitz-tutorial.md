---
title: 'Tutorial: Azure Active Directory integration with TiViTz | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TiViTz.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/07/2017
ms.author: jeedes
ms.openlocfilehash: afb14727009c12b23c86d775225dd290dad79807
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549785"
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="fbd75-103">Tutorial: Azure Active Directory integration with TiViTz</span><span class="sxs-lookup"><span data-stu-id="fbd75-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="fbd75-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbd75-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbd75-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fbd75-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbd75-106">You can control in Azure AD who has access to TiViTz</span><span class="sxs-lookup"><span data-stu-id="fbd75-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="fbd75-107">You can enable your users to automatically get signed-on to TiViTz single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="fbd75-107">You can enable your users to automatically get signed-on to TiViTz single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbd75-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="fbd75-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="fbd75-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbd75-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbd75-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fbd75-110">Prerequisites</span></span>

<span data-ttu-id="fbd75-111">To configure Azure AD integration with TiViTz, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fbd75-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="fbd75-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fbd75-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbd75-113">A TiViTz SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fbd75-113">A TiViTz SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="fbd75-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fbd75-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="fbd75-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fbd75-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbd75-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="fbd75-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fbd75-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbd75-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbd75-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fbd75-118">Scenario description</span></span>
<span data-ttu-id="fbd75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fbd75-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbd75-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fbd75-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbd75-121">Adding TiViTz from the gallery</span><span class="sxs-lookup"><span data-stu-id="fbd75-121">Adding TiViTz from the gallery</span></span>
2. <span data-ttu-id="fbd75-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="fbd75-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-tivitz-from-the-gallery"></a><span data-ttu-id="fbd75-123">Add TiViTz from the gallery</span><span class="sxs-lookup"><span data-stu-id="fbd75-123">Add TiViTz from the gallery</span></span>
<span data-ttu-id="fbd75-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fbd75-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbd75-125">**To add TiViTz from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fbd75-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbd75-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbd75-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fbd75-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="fbd75-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fbd75-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="fbd75-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fbd75-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="fbd75-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="fbd75-135">In the search box, type **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-135">In the search box, type **TiViTz**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_001.png)

7. <span data-ttu-id="fbd75-137">In the results pane, select **TiViTz**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="fbd75-137">In the results pane, select **TiViTz**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fbd75-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbd75-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="fbd75-140">In this section, you configure and test Azure AD SSO with TiViTz based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fbd75-140">In this section, you configure and test Azure AD SSO with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbd75-141">For SSO to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbd75-141">For SSO to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="fbd75-142">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fbd75-142">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="fbd75-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TiViTz.</span><span class="sxs-lookup"><span data-stu-id="fbd75-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TiViTz.</span></span>

<span data-ttu-id="fbd75-144">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fbd75-144">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbd75-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fbd75-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbd75-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbd75-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbd75-147">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="fbd75-147">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fbd75-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fbd75-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbd75-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fbd75-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fbd75-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbd75-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fbd75-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your TiViTz application.</span><span class="sxs-lookup"><span data-stu-id="fbd75-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="fbd75-152">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fbd75-152">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="fbd75-153">In the classic portal, on the **TiViTz** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="fbd75-153">In the classic portal, on the **TiViTz** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>

    ![Configure Single Sign-On][6]

2. <span data-ttu-id="fbd75-155">On the **How would you like users to sign on to TiViTz** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-155">On the **How would you like users to sign on to TiViTz** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_02.png)

3. <span data-ttu-id="fbd75-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbd75-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_03.png)
 1. <span data-ttu-id="fbd75-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="fbd75-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.o365.tivitz.com/`</span></span>
 2. <span data-ttu-id="fbd75-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="fbd75-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.o365.tivitz.com/`</span></span>
 3. <span data-ttu-id="fbd75-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-161">Click **Next**.</span></span>

     >[!NOTE] 
     ><span data-ttu-id="fbd75-162">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="fbd75-162">Please note that these are not the real values.</span></span> <span data-ttu-id="fbd75-163">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="fbd75-163">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="fbd75-164">Contact [TiViTz support team](emaiLto:info@tivitz.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="fbd75-164">Contact [TiViTz support team](emaiLto:info@tivitz.com) to get these values.</span></span>
     >

4. <span data-ttu-id="fbd75-165">On the **Configure single sign-on at TiViTz** page, click **Download metadata** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="fbd75-165">On the **Configure single sign-on at TiViTz** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_04.png) 

5. <span data-ttu-id="fbd75-167">To get SSO configured for your application, contact [TiViTz support team](emaiLto:info@tivitz.com) and provide them with the downloaded **Metadata**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-167">To get SSO configured for your application, contact [TiViTz support team](emaiLto:info@tivitz.com) and provide them with the downloaded **Metadata**.</span></span>

6. <span data-ttu-id="fbd75-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-168">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="fbd75-170">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fbd75-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fbd75-172">Create an Azure AD test user</span></span>
<span data-ttu-id="fbd75-173">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbd75-173">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="fbd75-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fbd75-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbd75-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-176">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="fbd75-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="fbd75-178">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="fbd75-179">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-179">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbd75-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-181">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="fbd75-183">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbd75-183">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="fbd75-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="fbd75-185">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="fbd75-186">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="fbd75-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-187">Click **Next**.</span></span>

6.  <span data-ttu-id="fbd75-188">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbd75-188">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="fbd75-190">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-190">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="fbd75-191">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-191">In the **Last Name** textbox, type, **Simon**.</span></span>
 3. <span data-ttu-id="fbd75-192">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-192">In the **Display Name** textbox, type **Britta Simon**.</span></span>
 4. <span data-ttu-id="fbd75-193">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-193">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="fbd75-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-194">Click **Next**.</span></span>

7. <span data-ttu-id="fbd75-195">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-195">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="fbd75-197">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbd75-197">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="fbd75-199">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-199">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="fbd75-200">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-200">Click **Complete**.</span></span>   

### <a name="create-a-tivitz-test-user"></a><span data-ttu-id="fbd75-201">Create a TiViTz test user</span><span class="sxs-lookup"><span data-stu-id="fbd75-201">Create a TiViTz test user</span></span>

<span data-ttu-id="fbd75-202">The objective of this section is to create a user called Britta Simon in TiViTz.</span><span class="sxs-lookup"><span data-stu-id="fbd75-202">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="fbd75-203">TiViTz supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="fbd75-203">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fbd75-204">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="fbd75-204">There is no action item for you in this section.</span></span> <span data-ttu-id="fbd75-205">A new user will be created during an attempt to access TiViTz if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="fbd75-205">A new user will be created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="fbd75-206">If you need to create an user manually, you need to contact [TiViTz support team](emaiLto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="fbd75-206">If you need to create an user manually, you need to contact [TiViTz support team](emaiLto:info@tivitz.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fbd75-207">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fbd75-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="fbd75-208">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to TiViTz.</span><span class="sxs-lookup"><span data-stu-id="fbd75-208">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to TiViTz.</span></span>

![Assign User][200] 

<span data-ttu-id="fbd75-210">**To assign Britta Simon to TiViTz, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fbd75-210">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="fbd75-211">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="fbd75-211">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="fbd75-213">In the applications list, select **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-213">In the applications list, select **TiViTz**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_50.png) 

3. <span data-ttu-id="fbd75-215">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-215">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="fbd75-217">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-217">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="fbd75-218">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="fbd75-218">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="fbd75-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fbd75-220">Test single sign-on</span></span>

<span data-ttu-id="fbd75-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fbd75-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fbd75-222">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span><span class="sxs-lookup"><span data-stu-id="fbd75-222">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbd75-223">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fbd75-223">Additional resources</span></span>

* [<span data-ttu-id="fbd75-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbd75-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbd75-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbd75-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tivitz-tutorial/tutorial_general_205.png

























