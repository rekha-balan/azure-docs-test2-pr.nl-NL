---
title: 'Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EthicsPoint Incident Management (EPIM).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 79e0dca01f4c4b68e90c87b8761bb66ef60d1bfb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563362"
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="99faa-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="99faa-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="99faa-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99faa-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99faa-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99faa-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="99faa-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="99faa-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="99faa-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="99faa-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99faa-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="99faa-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="99faa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99faa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99faa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99faa-110">Prerequisites</span></span>

<span data-ttu-id="99faa-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99faa-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span></span>

- <span data-ttu-id="99faa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99faa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99faa-113">A EthicsPoint Incident Management (EPIM) single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99faa-113">A EthicsPoint Incident Management (EPIM) single-sign on enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="99faa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="99faa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="99faa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99faa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99faa-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="99faa-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="99faa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99faa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="99faa-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="99faa-118">Scenario description</span></span>
<span data-ttu-id="99faa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99faa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="99faa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99faa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99faa-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span><span class="sxs-lookup"><span data-stu-id="99faa-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
2. <span data-ttu-id="99faa-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99faa-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a><span data-ttu-id="99faa-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span><span class="sxs-lookup"><span data-stu-id="99faa-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
<span data-ttu-id="99faa-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="99faa-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99faa-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99faa-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99faa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99faa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="99faa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99faa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="99faa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99faa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="99faa-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="99faa-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="99faa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="99faa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="99faa-135">In the search box, type **EthicsPoint Incident Management**.</span><span class="sxs-lookup"><span data-stu-id="99faa-135">In the search box, type **EthicsPoint Incident Management**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_01.png)

7. <span data-ttu-id="99faa-137">In the results pane, select **EthicsPoint Incident Management**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="99faa-137">In the results pane, select **EthicsPoint Incident Management**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99faa-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99faa-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99faa-140">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99faa-140">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99faa-141">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99faa-141">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span></span> <span data-ttu-id="99faa-142">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="99faa-142">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span></span>

<span data-ttu-id="99faa-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="99faa-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in EthicsPoint Incident Management (EPIM).</span></span>

<span data-ttu-id="99faa-144">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="99faa-144">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99faa-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="99faa-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99faa-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99faa-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99faa-147">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="99faa-147">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99faa-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99faa-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99faa-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="99faa-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99faa-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="99faa-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99faa-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span><span class="sxs-lookup"><span data-stu-id="99faa-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>


<span data-ttu-id="99faa-152">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99faa-152">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="99faa-153">In the classic portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="99faa-153">In the classic portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="99faa-155">On the **How would you like users to sign on to EthicsPoint Incident Management (EPIM)** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99faa-155">On the **How would you like users to sign on to EthicsPoint Incident Management (EPIM)** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_03.png) 

3. <span data-ttu-id="99faa-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99faa-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_04.png) 

    <span data-ttu-id="99faa-159">a.</span><span class="sxs-lookup"><span data-stu-id="99faa-159">a.</span></span> <span data-ttu-id="99faa-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your EthicsPoint Incident Management (EPIM) application using the following pattern: `https://<companyname>.navexglobal.com` or `https://<companyname>.ethicspointvp.com`</span><span class="sxs-lookup"><span data-stu-id="99faa-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your EthicsPoint Incident Management (EPIM) application using the following pattern: `https://<companyname>.navexglobal.com` or `https://<companyname>.ethicspointvp.com`</span></span>
    
    <span data-ttu-id="99faa-161">b.</span><span class="sxs-lookup"><span data-stu-id="99faa-161">b.</span></span> <span data-ttu-id="99faa-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="99faa-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    <span data-ttu-id="99faa-163">c.</span><span class="sxs-lookup"><span data-stu-id="99faa-163">c.</span></span> <span data-ttu-id="99faa-164">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="99faa-164">Click **Next**</span></span>
 
4. <span data-ttu-id="99faa-165">On the **Configure single sign-on at EthicsPoint Incident Management (EPIM)** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99faa-165">On the **Configure single sign-on at EthicsPoint Incident Management (EPIM)** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_05.png)

    <span data-ttu-id="99faa-167">a.</span><span class="sxs-lookup"><span data-stu-id="99faa-167">a.</span></span> <span data-ttu-id="99faa-168">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="99faa-168">Click **Download metadata**, and then save the file on your computer.</span></span>

    <span data-ttu-id="99faa-169">b.</span><span class="sxs-lookup"><span data-stu-id="99faa-169">b.</span></span> <span data-ttu-id="99faa-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99faa-170">Click **Next**.</span></span>


5. <span data-ttu-id="99faa-171">To get SSO configured for your application, contact EthicsPoint Incident Management (EPIM) support team and provide them with the downloaded **metadata** file.</span><span class="sxs-lookup"><span data-stu-id="99faa-171">To get SSO configured for your application, contact EthicsPoint Incident Management (EPIM) support team and provide them with the downloaded **metadata** file.</span></span>

6. <span data-ttu-id="99faa-172">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99faa-172">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="99faa-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99faa-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99faa-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99faa-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="99faa-177">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99faa-177">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Create Azure AD User][20]

<span data-ttu-id="99faa-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99faa-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99faa-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99faa-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="99faa-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99faa-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="99faa-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99faa-183">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99faa-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="99faa-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="99faa-187">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="99faa-187">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="99faa-188">a.</span><span class="sxs-lookup"><span data-stu-id="99faa-188">a.</span></span> <span data-ttu-id="99faa-189">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="99faa-189">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="99faa-190">b.</span><span class="sxs-lookup"><span data-stu-id="99faa-190">b.</span></span> <span data-ttu-id="99faa-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99faa-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99faa-192">c.</span><span class="sxs-lookup"><span data-stu-id="99faa-192">c.</span></span> <span data-ttu-id="99faa-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99faa-193">Click **Next**.</span></span>

6.  <span data-ttu-id="99faa-194">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="99faa-194">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="99faa-195">a.</span><span class="sxs-lookup"><span data-stu-id="99faa-195">a.</span></span> <span data-ttu-id="99faa-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="99faa-196">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="99faa-197">b.</span><span class="sxs-lookup"><span data-stu-id="99faa-197">b.</span></span> <span data-ttu-id="99faa-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="99faa-198">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="99faa-199">c.</span><span class="sxs-lookup"><span data-stu-id="99faa-199">c.</span></span> <span data-ttu-id="99faa-200">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99faa-200">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="99faa-201">d.</span><span class="sxs-lookup"><span data-stu-id="99faa-201">d.</span></span> <span data-ttu-id="99faa-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="99faa-202">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="99faa-203">e.</span><span class="sxs-lookup"><span data-stu-id="99faa-203">e.</span></span> <span data-ttu-id="99faa-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99faa-204">Click **Next**.</span></span>

7. <span data-ttu-id="99faa-205">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="99faa-205">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="99faa-207">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99faa-207">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="99faa-209">a.</span><span class="sxs-lookup"><span data-stu-id="99faa-209">a.</span></span> <span data-ttu-id="99faa-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="99faa-210">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="99faa-211">b.</span><span class="sxs-lookup"><span data-stu-id="99faa-211">b.</span></span> <span data-ttu-id="99faa-212">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99faa-212">Click **Complete**.</span></span>   



### <a name="creating-an-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="99faa-213">Creating an EthicsPoint Incident Management (EPIM) test user</span><span class="sxs-lookup"><span data-stu-id="99faa-213">Creating an EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="99faa-214">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="99faa-214">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="99faa-215">Please work with EthicsPoint Incident Management (EPIM) support team to add the users in the EthicsPoint Incident Management (EPIM) platform.</span><span class="sxs-lookup"><span data-stu-id="99faa-215">Please work with EthicsPoint Incident Management (EPIM) support team to add the users in the EthicsPoint Incident Management (EPIM) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="99faa-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99faa-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="99faa-217">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="99faa-217">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to EthicsPoint Incident Management (EPIM).</span></span>

![Assign User][200] 

<span data-ttu-id="99faa-219">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99faa-219">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="99faa-220">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99faa-220">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="99faa-222">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="99faa-222">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspointincidentmanagement_50.png) 

3. <span data-ttu-id="99faa-224">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99faa-224">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="99faa-226">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99faa-226">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="99faa-227">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="99faa-227">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="99faa-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="99faa-229">Testing single sign-on</span></span>

<span data-ttu-id="99faa-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99faa-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99faa-231">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span><span class="sxs-lookup"><span data-stu-id="99faa-231">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="99faa-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="99faa-232">Additional resources</span></span>

* [<span data-ttu-id="99faa-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99faa-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99faa-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99faa-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_205.png
























