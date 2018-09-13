---
title: 'Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Splunk Enterprise and Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: c90d0e6d4a4d85f556dc3c9bae09989d6211e30c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563435"
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="3b76d-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="3b76d-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="3b76d-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b76d-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b76d-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3b76d-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3b76d-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="3b76d-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="3b76d-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3b76d-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b76d-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="3b76d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3b76d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b76d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b76d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b76d-110">Prerequisites</span></span>

<span data-ttu-id="3b76d-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3b76d-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="3b76d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3b76d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b76d-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3b76d-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="3b76d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3b76d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="3b76d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3b76d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b76d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3b76d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3b76d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b76d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3b76d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3b76d-118">Scenario description</span></span>
<span data-ttu-id="3b76d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3b76d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="3b76d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3b76d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b76d-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3b76d-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="3b76d-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3b76d-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="3b76d-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="3b76d-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="3b76d-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3b76d-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3b76d-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3b76d-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3b76d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="3b76d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3b76d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3b76d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3b76d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="3b76d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3b76d-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="3b76d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="3b76d-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="3b76d-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3b76d-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3b76d-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3b76d-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3b76d-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3b76d-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b76d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b76d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="3b76d-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3b76d-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="3b76d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="3b76d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="3b76d-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3b76d-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3b76d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3b76d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3b76d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b76d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b76d-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3b76d-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3b76d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3b76d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b76d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3b76d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3b76d-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3b76d-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3b76d-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3b76d-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="3b76d-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3b76d-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3b76d-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="3b76d-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="3b76d-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="3b76d-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3b76d-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="3b76d-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="3b76d-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="3b76d-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="3b76d-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="3b76d-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="3b76d-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="3b76d-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="3b76d-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3b76d-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="3b76d-165">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3b76d-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="3b76d-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-166">Click **Next**.</span></span>

5. <span data-ttu-id="3b76d-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="3b76d-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="3b76d-168">The downloaded **federaton metadata**</span><span class="sxs-lookup"><span data-stu-id="3b76d-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="3b76d-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="3b76d-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3b76d-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3b76d-173">Create an Azure AD test user</span></span>
<span data-ttu-id="3b76d-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b76d-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="3b76d-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3b76d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3b76d-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3b76d-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3b76d-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="3b76d-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b76d-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3b76d-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3b76d-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="3b76d-186">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="3b76d-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="3b76d-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="3b76d-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-188">Click **Next**.</span></span>

6.  <span data-ttu-id="3b76d-189">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3b76d-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="3b76d-191">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="3b76d-192">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="3b76d-193">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="3b76d-194">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="3b76d-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-195">Click **Next**.</span></span>

7. <span data-ttu-id="3b76d-196">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3b76d-198">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3b76d-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="3b76d-200">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="3b76d-201">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="3b76d-202">Create a Splunk Enterprise and Splunk Cloud test user</span><span class="sxs-lookup"><span data-stu-id="3b76d-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="3b76d-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="3b76d-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="3b76d-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="3b76d-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3b76d-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3b76d-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="3b76d-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="3b76d-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="3b76d-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3b76d-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="3b76d-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3b76d-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3b76d-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="3b76d-213">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-213">In the menu on the top, click **Users**.</span></span>

    ![Assign User][203]

4. <span data-ttu-id="3b76d-215">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3b76d-216">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3b76d-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3b76d-218">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3b76d-218">Test single sign-on</span></span>

<span data-ttu-id="3b76d-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3b76d-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="3b76d-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span><span class="sxs-lookup"><span data-stu-id="3b76d-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3b76d-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3b76d-221">Additional resources</span></span>

* [<span data-ttu-id="3b76d-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b76d-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b76d-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b76d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png

























