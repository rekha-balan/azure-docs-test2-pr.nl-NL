---
title: 'Tutorial: Azure Active Directory integration with Bridge | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 2fdfcde8dbf7cf9fdaf47ab0c98861940c75980a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553752"
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="3ae61-103">Tutorial: Azure Active Directory integration with Bridge</span><span class="sxs-lookup"><span data-stu-id="3ae61-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="3ae61-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ae61-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ae61-105">Integrating Bridge with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3ae61-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ae61-106">You can control in Azure AD who has access to Bridge</span><span class="sxs-lookup"><span data-stu-id="3ae61-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="3ae61-107">You can enable your users to automatically get signed-on to Bridge single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3ae61-107">You can enable your users to automatically get signed-on to Bridge single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ae61-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="3ae61-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3ae61-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ae61-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ae61-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3ae61-110">Prerequisites</span></span>

<span data-ttu-id="3ae61-111">To configure Azure AD integration with Bridge, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3ae61-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="3ae61-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3ae61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ae61-113">A Bridge SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3ae61-113">A Bridge SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="3ae61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3ae61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="3ae61-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3ae61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ae61-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3ae61-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3ae61-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ae61-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3ae61-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3ae61-118">Scenario description</span></span>
<span data-ttu-id="3ae61-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3ae61-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="3ae61-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ae61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ae61-121">Adding Bridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ae61-121">Adding Bridge from the gallery</span></span>
2. <span data-ttu-id="3ae61-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3ae61-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-bridge-from-the-gallery"></a><span data-ttu-id="3ae61-123">Add Bridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="3ae61-123">Add Bridge from the gallery</span></span>
<span data-ttu-id="3ae61-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3ae61-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ae61-125">**To add Bridge from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ae61-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ae61-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ae61-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3ae61-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3ae61-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3ae61-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="3ae61-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3ae61-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="3ae61-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="3ae61-135">In the search box, type **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-135">In the search box, type **Bridge**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_001.png)

7. <span data-ttu-id="3ae61-137">In the results pane, select **Bridge**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3ae61-137">In the results pane, select **Bridge**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_0001.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3ae61-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ae61-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3ae61-140">In this section, you configure and test Azure AD SSO with Bridge based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ae61-140">In this section, you configure and test Azure AD SSO with Bridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ae61-141">For SSO to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ae61-141">For SSO to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="3ae61-142">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3ae61-142">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="3ae61-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bridge.</span><span class="sxs-lookup"><span data-stu-id="3ae61-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bridge.</span></span>

<span data-ttu-id="3ae61-144">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3ae61-144">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ae61-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3ae61-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ae61-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ae61-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ae61-147">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3ae61-147">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3ae61-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3ae61-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ae61-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3ae61-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3ae61-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ae61-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3ae61-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Bridge application.</span><span class="sxs-lookup"><span data-stu-id="3ae61-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Bridge application.</span></span>


<span data-ttu-id="3ae61-152">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ae61-152">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="3ae61-153">In the classic portal, on the **Bridge** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="3ae61-153">In the classic portal, on the **Bridge** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>

    ![Configure Single Sign-On][6]

2. <span data-ttu-id="3ae61-155">On the **How would you like users to sign on to Bridge** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-155">On the **How would you like users to sign on to Bridge** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_02.png)

3. <span data-ttu-id="3ae61-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ae61-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_03.png)
  1. <span data-ttu-id="3ae61-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="3ae61-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>
  2. <span data-ttu-id="3ae61-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="3ae61-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>
  3. <span data-ttu-id="3ae61-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-161">Click **Next**.</span></span>

    >[!NOTE] 
    ><span data-ttu-id="3ae61-162">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="3ae61-162">Please note that these are not the real values.</span></span> <span data-ttu-id="3ae61-163">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="3ae61-163">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="3ae61-164">You can raise the support ticket with Bridge from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> to get these values.</span><span class="sxs-lookup"><span data-stu-id="3ae61-164">You can raise the support ticket with Bridge from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> to get these values.</span></span>
    >

4. <span data-ttu-id="3ae61-165">On the **Configure single sign-on at Bridge** page, click **Download certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="3ae61-165">On the **Configure single sign-on at Bridge** page, click **Download certificate** and then save the file on your computer:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_04.png) 

5. <span data-ttu-id="3ae61-167">To get SSO configured for your application, You can raise the support ticket with Bridge  support team from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="3ae61-167">To get SSO configured for your application, You can raise the support ticket with Bridge  support team from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> and provide them with the following:</span></span> 

 *  <span data-ttu-id="3ae61-168">The downloaded **certificate file**</span><span class="sxs-lookup"><span data-stu-id="3ae61-168">The downloaded **certificate file**</span></span>
 *  <span data-ttu-id="3ae61-169">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="3ae61-169">The **Entity ID**</span></span>
 *  <span data-ttu-id="3ae61-170">The **Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="3ae61-170">The **Single Sign-On Service URL**</span></span>
 *  <span data-ttu-id="3ae61-171">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="3ae61-171">The **Single Sign-Out Service URL**</span></span>

6. <span data-ttu-id="3ae61-172">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-172">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="3ae61-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3ae61-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ae61-176">Create an Azure AD test user</span></span>
<span data-ttu-id="3ae61-177">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ae61-177">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="3ae61-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ae61-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ae61-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3ae61-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3ae61-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3ae61-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-183">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ae61-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3ae61-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ae61-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="3ae61-189">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="3ae61-189">As Type Of User, select New user in your organization.</span></span>
 2. <span data-ttu-id="3ae61-190">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-190">In the User Name **textbox**, type **BrittaSimon**.</span></span>
 3. <span data-ttu-id="3ae61-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-191">Click **Next**.</span></span>

6.  <span data-ttu-id="3ae61-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ae61-192">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="3ae61-194">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-194">In the **First Name** textbox, type **Britta**.</span></span>  
 2. <span data-ttu-id="3ae61-195">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-195">In the **Last Name** textbox, type, **Simon**.</span></span>
 3. <span data-ttu-id="3ae61-196">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
 4. <span data-ttu-id="3ae61-197">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-197">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="3ae61-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-198">Click **Next**.</span></span>

7. <span data-ttu-id="3ae61-199">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-199">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3ae61-201">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3ae61-201">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="3ae61-203">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-203">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="3ae61-204">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-204">Click **Complete**.</span></span>   

### <a name="create-a-bridge-test-user"></a><span data-ttu-id="3ae61-205">Create a Bridge test user</span><span class="sxs-lookup"><span data-stu-id="3ae61-205">Create a Bridge test user</span></span>

<span data-ttu-id="3ae61-206">In this section, you create a user called Britta Simon in Bridge.</span><span class="sxs-lookup"><span data-stu-id="3ae61-206">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="3ae61-207">Please work with Bridge support team to create a user in the platform.</span><span class="sxs-lookup"><span data-stu-id="3ae61-207">Please work with Bridge support team to create a user in the platform.</span></span> <span data-ttu-id="3ae61-208">You can raise the support ticket with Bridge from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> to add the users in the Bridge platform.</span><span class="sxs-lookup"><span data-stu-id="3ae61-208">You can raise the support ticket with Bridge from <a href="https://bridgeapp.zendesk.com/hc/en-us/requests/new">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3ae61-209">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3ae61-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="3ae61-210">In this section, you enable Britta Simon to use Azure SSO by granting her access to Bridge.</span><span class="sxs-lookup"><span data-stu-id="3ae61-210">In this section, you enable Britta Simon to use Azure SSO by granting her access to Bridge.</span></span>

![Assign User][200] 

<span data-ttu-id="3ae61-212">**To assign Britta Simon to Bridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3ae61-212">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="3ae61-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3ae61-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3ae61-215">In the applications list, select **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-215">In the applications list, select **Bridge**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_bridge_50.png) 

3. <span data-ttu-id="3ae61-217">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-217">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203] 

4. <span data-ttu-id="3ae61-219">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-219">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3ae61-220">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3ae61-220">In the toolbar on the bottom, click **Assign**.</span></span>
    
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3ae61-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3ae61-222">Test single sign-on</span></span>

<span data-ttu-id="3ae61-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3ae61-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3ae61-224">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span><span class="sxs-lookup"><span data-stu-id="3ae61-224">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ae61-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3ae61-225">Additional resources</span></span>

* [<span data-ttu-id="3ae61-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ae61-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ae61-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ae61-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bridge-tutorial/tutorial_general_205.png

























