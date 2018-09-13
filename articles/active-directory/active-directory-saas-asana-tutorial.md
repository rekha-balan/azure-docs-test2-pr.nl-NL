---
title: 'Tutorial: Azure Active Directory integration with Asana | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Asana.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: ffd2bb4bce1c4588641dfc77aa0086d0a10fc317
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562925"
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="2ee97-103">Tutorial: Azure Active Directory integration with Asana</span><span class="sxs-lookup"><span data-stu-id="2ee97-103">Tutorial: Azure Active Directory integration with Asana</span></span>
<span data-ttu-id="2ee97-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ee97-104">In this tutorial, you learn how to integrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ee97-105">Integrating Asana with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2ee97-105">Integrating Asana with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="2ee97-106">You can control in Azure AD who has access to Asana</span><span class="sxs-lookup"><span data-stu-id="2ee97-106">You can control in Azure AD who has access to Asana</span></span>
* <span data-ttu-id="2ee97-107">You can enable your users to automatically get signed-on to Asana single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2ee97-107">You can enable your users to automatically get signed-on to Asana single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="2ee97-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="2ee97-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="2ee97-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ee97-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ee97-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ee97-110">Prerequisites</span></span>
<span data-ttu-id="2ee97-111">To configure Azure AD integration with Asana, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2ee97-111">To configure Azure AD integration with Asana, you need the following items:</span></span>

* <span data-ttu-id="2ee97-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2ee97-112">An Azure AD subscription</span></span>
* <span data-ttu-id="2ee97-113">A **Asana** single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2ee97-113">A **Asana** single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="2ee97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2ee97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="2ee97-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2ee97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2ee97-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="2ee97-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2ee97-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ee97-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ee97-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2ee97-118">Scenario description</span></span>
<span data-ttu-id="2ee97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2ee97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ee97-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2ee97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ee97-121">Adding Asana from the gallery</span><span class="sxs-lookup"><span data-stu-id="2ee97-121">Adding Asana from the gallery</span></span>
2. <span data-ttu-id="2ee97-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="2ee97-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-asana-from-the-gallery"></a><span data-ttu-id="2ee97-123">Adding Asana from the gallery</span><span class="sxs-lookup"><span data-stu-id="2ee97-123">Adding Asana from the gallery</span></span>
<span data-ttu-id="2ee97-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2ee97-124">To configure the integration of Asana into Azure AD, you need to add Asana from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ee97-125">**To add Asana from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2ee97-125">**To add Asana from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee97-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="2ee97-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2ee97-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2ee97-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2ee97-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="2ee97-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2ee97-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="2ee97-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="2ee97-135">In the search box, type **Asana**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-135">In the search box, type **Asana**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_01.png)
7. <span data-ttu-id="2ee97-137">In the results pane, select **Asana**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="2ee97-137">In the results pane, select **Asana**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="2ee97-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="2ee97-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="2ee97-140">In this section, you configure and test Azure AD SSO with Asana based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2ee97-140">In this section, you configure and test Azure AD SSO with Asana based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ee97-141">For SSO to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ee97-141">For SSO to work, Azure AD needs to know what the counterpart user in Asana is to a user in Azure AD.</span></span> <span data-ttu-id="2ee97-142">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2ee97-142">In other words, a link relationship between an Azure AD user and the related user in Asana needs to be established.</span></span>

<span data-ttu-id="2ee97-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Asana.</span><span class="sxs-lookup"><span data-stu-id="2ee97-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Asana.</span></span>

<span data-ttu-id="2ee97-144">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2ee97-144">To configure and test Azure AD single sign-on with Asana, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ee97-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2ee97-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ee97-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ee97-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ee97-147">**[Creating an Asana test user](#creating-an-Asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="2ee97-147">**[Creating an Asana test user](#creating-an-Asana-test-user)** - to have a counterpart of Britta Simon in Asana that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2ee97-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2ee97-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ee97-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2ee97-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="2ee97-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="2ee97-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="2ee97-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Asana application.</span><span class="sxs-lookup"><span data-stu-id="2ee97-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Asana application.</span></span>

<span data-ttu-id="2ee97-152">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2ee97-152">**To configure Azure AD single sign-on with Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee97-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="2ee97-155">In the classic portal, on the **Asana** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="2ee97-155">In the classic portal, on the **Asana** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
3. <span data-ttu-id="2ee97-157">On the **How would you like users to sign on to Asana** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-157">On the **How would you like users to sign on to Asana** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_06.png)
4. <span data-ttu-id="2ee97-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ee97-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_07.png)
  1. <span data-ttu-id="2ee97-161">In the Sign On URL textbox, type a URL using the following pattern: `https://app.asana.com`</span><span class="sxs-lookup"><span data-stu-id="2ee97-161">In the Sign On URL textbox, type a URL using the following pattern: `https://app.asana.com`</span></span>
  2. <span data-ttu-id="2ee97-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-162">Click **Next**.</span></span>
5. <span data-ttu-id="2ee97-163">On the **Configure single sign-on at Asana** page, Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2ee97-163">On the **Configure single sign-on at Asana** page, Click **Download certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="2ee97-164">Also, copy the value for SAML SSO URL.</span><span class="sxs-lookup"><span data-stu-id="2ee97-164">Also, copy the value for SAML SSO URL.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_08.png)
6. <span data-ttu-id="2ee97-166">Right click on the certificate, then open the certificate file using Notepad or you preferred text editor.</span><span class="sxs-lookup"><span data-stu-id="2ee97-166">Right click on the certificate, then open the certificate file using Notepad or you preferred text editor.</span></span> <span data-ttu-id="2ee97-167">Copy the content between the begin and the end certificate title.</span><span class="sxs-lookup"><span data-stu-id="2ee97-167">Copy the content between the begin and the end certificate title.</span></span> <span data-ttu-id="2ee97-168">This is the X.509 certificate you will use in Asana to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="2ee97-168">This is the X.509 certificate you will use in Asana to configure SSO.</span></span>
7. <span data-ttu-id="2ee97-169">In a different browser window, sign-on to your Asana application.</span><span class="sxs-lookup"><span data-stu-id="2ee97-169">In a different browser window, sign-on to your Asana application.</span></span> <span data-ttu-id="2ee97-170">To configure SSO in Asana, access the workspace settings by clicking on the workspace name on the top right corner of the screen.</span><span class="sxs-lookup"><span data-stu-id="2ee97-170">To configure SSO in Asana, access the workspace settings by clicking on the workspace name on the top right corner of the screen.</span></span> <span data-ttu-id="2ee97-171">Then, click on **\<your workspace name\> Settings**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-171">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)
8. <span data-ttu-id="2ee97-173">On the **Organization settings** window, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-173">On the **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="2ee97-174">Then, click **Members must log in via SAML** to enable the SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="2ee97-174">Then, click **Members must log in via SAML** to enable the SSO configuration.</span></span> <span data-ttu-id="2ee97-175">The perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ee97-175">The perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  
  1. <span data-ttu-id="2ee97-177">In the **Sign-in page URL** texbox, paste the SAML Sign on URL from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ee97-177">In the **Sign-in page URL** texbox, paste the SAML Sign on URL from Azure AD.</span></span>
  2. <span data-ttu-id="2ee97-178">In the **X.509 Certificate** textbox, paste the X.509 Certificate you have copied from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ee97-178">In the **X.509 Certificate** textbox, paste the X.509 Certificate you have copied from Azure AD.</span></span>
9. <span data-ttu-id="2ee97-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-179">Click **Save**.</span></span> <span data-ttu-id="2ee97-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span><span class="sxs-lookup"><span data-stu-id="2ee97-180">Go to [Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>
10. <span data-ttu-id="2ee97-181">Go to **Configure single sign-on at Asana** page in Azure AD, select the SSO configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-181">Go to **Configure single sign-on at Asana** page in Azure AD, select the SSO configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="2ee97-183">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2ee97-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2ee97-185">Create an Azure AD test user</span></span>
<span data-ttu-id="2ee97-186">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ee97-186">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="2ee97-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2ee97-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee97-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="2ee97-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2ee97-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2ee97-192">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="2ee97-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="2ee97-196">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ee97-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="2ee97-198">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="2ee97-198">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="2ee97-199">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-199">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="2ee97-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-200">Click **Next**.</span></span>
6. <span data-ttu-id="2ee97-201">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ee97-201">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="2ee97-203">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-203">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="2ee97-204">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-204">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="2ee97-205">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-205">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="2ee97-206">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-206">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="2ee97-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-207">Click **Next**.</span></span>
7. <span data-ttu-id="2ee97-208">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-208">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="2ee97-210">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ee97-210">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="2ee97-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-212">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="2ee97-213">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-213">Click **Complete**.</span></span>   

### <a name="create-an-asana-test-user"></a><span data-ttu-id="2ee97-214">Create an Asana test user</span><span class="sxs-lookup"><span data-stu-id="2ee97-214">Create an Asana test user</span></span>
<span data-ttu-id="2ee97-215">In this section, you create a user called Britta Simon in Asana.</span><span class="sxs-lookup"><span data-stu-id="2ee97-215">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="2ee97-216">On **Asana**, go to the **Teams** section on the left panel.</span><span class="sxs-lookup"><span data-stu-id="2ee97-216">On **Asana**, go to the **Teams** section on the left panel.</span></span> <span data-ttu-id="2ee97-217">Click the plus sign button.</span><span class="sxs-lookup"><span data-stu-id="2ee97-217">Click the plus sign button.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 
2. <span data-ttu-id="2ee97-219">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-219">Type the email britta.simon@contoso.com in the text box and then select **Invite**.</span></span>
3. <span data-ttu-id="2ee97-220">Click **Send Invite**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-220">Click **Send Invite**.</span></span> <span data-ttu-id="2ee97-221">The new user will receive an email into her email account.</span><span class="sxs-lookup"><span data-stu-id="2ee97-221">The new user will receive an email into her email account.</span></span> <span data-ttu-id="2ee97-222">She will need to create and validate the account.</span><span class="sxs-lookup"><span data-stu-id="2ee97-222">She will need to create and validate the account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2ee97-223">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2ee97-223">Assign the Azure AD test user</span></span>
<span data-ttu-id="2ee97-224">In this section, you enable Britta Simon to use Azure SSO by granting her access to Asana.</span><span class="sxs-lookup"><span data-stu-id="2ee97-224">In this section, you enable Britta Simon to use Azure SSO by granting her access to Asana.</span></span>

![Assign User][200] 

<span data-ttu-id="2ee97-226">**To assign Britta Simon to Asana, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2ee97-226">**To assign Britta Simon to Asana, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee97-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2ee97-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="2ee97-229">In the applications list, select **Asana**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-229">In the applications list, select **Asana**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_asana_50.png) 
3. <span data-ttu-id="2ee97-231">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-231">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="2ee97-233">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-233">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="2ee97-234">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-234">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="2ee97-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2ee97-236">Test single sign-on</span></span>
<span data-ttu-id="2ee97-237">The objective of this section is to test your Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2ee97-237">The objective of this section is to test your Azure AD single sign-on.</span></span>

<span data-ttu-id="2ee97-238">Go to Asana login page.</span><span class="sxs-lookup"><span data-stu-id="2ee97-238">Go to Asana login page.</span></span> <span data-ttu-id="2ee97-239">In the Email address textbox insert the email address britta.simon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ee97-239">In the Email address textbox insert the email address britta.simon@contoso.com.</span></span> <span data-ttu-id="2ee97-240">Leave the password textbox in blank and then click **Log In**.</span><span class="sxs-lookup"><span data-stu-id="2ee97-240">Leave the password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="2ee97-241">You will be redirected to Azure AD login page.</span><span class="sxs-lookup"><span data-stu-id="2ee97-241">You will be redirected to Azure AD login page.</span></span> <span data-ttu-id="2ee97-242">Complete your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="2ee97-242">Complete your Azure AD credentials.</span></span> <span data-ttu-id="2ee97-243">Now, you are logged in on Asana.</span><span class="sxs-lookup"><span data-stu-id="2ee97-243">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ee97-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2ee97-244">Additional resources</span></span>
* [<span data-ttu-id="2ee97-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ee97-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ee97-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ee97-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-asana-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-asana-tutorial/tutorial_general_205.png






























