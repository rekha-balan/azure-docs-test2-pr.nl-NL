---
title: 'Tutorial: Azure Active Directory integration with MOVEit Transfer | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and MOVEit Transfer.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: b47010195763905fe4402a4c8aea058e197a65d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660674"
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer"></a><span data-ttu-id="e9b3a-103">Tutorial: Azure Active Directory integration with MOVEit Transfer</span><span class="sxs-lookup"><span data-stu-id="e9b3a-103">Tutorial: Azure Active Directory integration with MOVEit Transfer</span></span>
<span data-ttu-id="e9b3a-104">The objective of this tutorial is to show you how to integrate MOVEit Transfer with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9b3a-104">The objective of this tutorial is to show you how to integrate MOVEit Transfer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9b3a-105">Integrating MOVEit Transfer with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-105">Integrating MOVEit Transfer with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e9b3a-106">You can control in Azure AD who has access to MOVEit Transfer</span><span class="sxs-lookup"><span data-stu-id="e9b3a-106">You can control in Azure AD who has access to MOVEit Transfer</span></span>
* <span data-ttu-id="e9b3a-107">You can enable your users to automatically get signed-on to MOVEit Transfer single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e9b3a-107">You can enable your users to automatically get signed-on to MOVEit Transfer single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="e9b3a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e9b3a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e9b3a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9b3a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9b3a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9b3a-110">Prerequisites</span></span>
<span data-ttu-id="e9b3a-111">To configure Azure AD integration with MOVEit Transfer, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-111">To configure Azure AD integration with MOVEit Transfer, you need the following items:</span></span>

* <span data-ttu-id="e9b3a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e9b3a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e9b3a-113">A MOVEit Transfer SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e9b3a-113">A MOVEit Transfer SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9b3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e9b3a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e9b3a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e9b3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9b3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9b3a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e9b3a-118">Scenario description</span></span>
<span data-ttu-id="e9b3a-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e9b3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9b3a-121">Adding MOVEit Transfer from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9b3a-121">Adding MOVEit Transfer from the gallery</span></span>
2. <span data-ttu-id="e9b3a-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9b3a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-moveit-transfer-from-the-gallery"></a><span data-ttu-id="e9b3a-123">Adding MOVEit Transfer from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9b3a-123">Adding MOVEit Transfer from the gallery</span></span>
<span data-ttu-id="e9b3a-124">To configure the integration of MOVEit Transfer into Azure AD, you need to add MOVEit Transfer from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-124">To configure the integration of MOVEit Transfer into Azure AD, you need to add MOVEit Transfer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9b3a-125">**To add MOVEit Transfer from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9b3a-125">**To add MOVEit Transfer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b3a-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="e9b3a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9b3a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="e9b3a-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e9b3a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="e9b3a-135">In the search box, type **MOVEit Transfer**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-135">In the search box, type **MOVEit Transfer**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_01.png)
7. <span data-ttu-id="e9b3a-137">In the results panel, select **MOVEit Transfer**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-137">In the results panel, select **MOVEit Transfer**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="e9b3a-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9b3a-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="e9b3a-140">The objective of this section is to show you how to configure and test Azure AD SSO with MOVEit Transfer based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9b3a-140">The objective of this section is to show you how to configure and test Azure AD SSO with MOVEit Transfer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9b3a-141">For SSO to work, Azure AD needs to know what the counterpart user in MOVEit Transfer to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-141">For SSO to work, Azure AD needs to know what the counterpart user in MOVEit Transfer to an user in Azure AD is.</span></span> <span data-ttu-id="e9b3a-142">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-142">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer needs to be established.</span></span>

<span data-ttu-id="e9b3a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MOVEit Transfer.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MOVEit Transfer.</span></span>

<span data-ttu-id="e9b3a-144">To configure and test Azure AD SSO with MOVEit Transfer, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-144">To configure and test Azure AD SSO with MOVEit Transfer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9b3a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9b3a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9b3a-147">**[Creating a MOVEit Transfer test user](#creating-a-moveit-transfer-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-147">**[Creating a MOVEit Transfer test user](#creating-a-moveit-transfer-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e9b3a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9b3a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="e9b3a-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9b3a-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="e9b3a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your MOVEit Transfer application.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your MOVEit Transfer application.</span></span>

<span data-ttu-id="e9b3a-152">**To configure Azure AD single sign-on with MOVEit Transfer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9b3a-152">**To configure Azure AD single sign-on with MOVEit Transfer, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b3a-153">In the classic portal, on the **MOVEit Transfer** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-153">In the classic portal, on the **MOVEit Transfer** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="e9b3a-155">On the **How would you like users to sign on to MOVEit Transfer** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-155">On the **How would you like users to sign on to MOVEit Transfer** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_03.png)
3. <span data-ttu-id="e9b3a-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_04.png)
  1. <span data-ttu-id="e9b3a-159">In the **Sign On URL** textbox, type sign in URL with your own domain.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-159">In the **Sign On URL** textbox, type sign in URL with your own domain.</span></span>
  2. <span data-ttu-id="e9b3a-160">In the **Identifier** textbox, type a entity ID URL.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-160">In the **Identifier** textbox, type a entity ID URL.</span></span>
  3. <span data-ttu-id="e9b3a-161">In the **REPLY URL** textbox, type a enebled Assertion Consumer Interface URL.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-161">In the **REPLY URL** textbox, type a enebled Assertion Consumer Interface URL.</span></span>
  4. <span data-ttu-id="e9b3a-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-162">Click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e9b3a-163">Please note that you have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-163">Please note that you have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="e9b3a-164">To get these values, you can refer step 8 for more details or contact [MOVEit Transfer](https://www.ipswitch.com/support/technical-support).</span><span class="sxs-lookup"><span data-stu-id="e9b3a-164">To get these values, you can refer step 8 for more details or contact [MOVEit Transfer](https://www.ipswitch.com/support/technical-support).</span></span>
   >  
4. <span data-ttu-id="e9b3a-165">On the **Configure single sign-on at MOVEit Transfer** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-165">On the **Configure single sign-on at MOVEit Transfer** page, perform the following steps and click **Next**:</span></span>
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_05.png)  
  1. <span data-ttu-id="e9b3a-167">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-167">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="e9b3a-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-168">Click **Next**.</span></span>
5. <span data-ttu-id="e9b3a-169">Sign-on to your MOVEit Transfer tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-169">Sign-on to your MOVEit Transfer tenant as an administrator.</span></span>
6. <span data-ttu-id="e9b3a-170">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-170">On the left navigation pane, click **Settings**.</span></span>
   
  ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)
7. <span data-ttu-id="e9b3a-172">Click **Single Signon** link which is under **Security Policies -> User Auth**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-172">Click **Single Signon** link which is under **Security Policies -> User Auth**.</span></span>
   
  ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)
8. <span data-ttu-id="e9b3a-174">Click the Metadata URL link to download the metadata document.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-174">Click the Metadata URL link to download the metadata document.</span></span>
   
  ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)   
  * <span data-ttu-id="e9b3a-176">Verify **entityID** matches **Identifier** in step3.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-176">Verify **entityID** matches **Identifier** in step3.</span></span>
  * <span data-ttu-id="e9b3a-177">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in step3.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-177">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in step3.</span></span>
     
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)
9. <span data-ttu-id="e9b3a-179">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-179">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>
   
  ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)
10. <span data-ttu-id="e9b3a-181">Click **Browse...** to select the metadata file which you downloaded in step 4,then click **Add Identity Provider** to upload the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-181">Click **Browse...** to select the metadata file which you downloaded in step 4,then click **Add Identity Provider** to upload the downloaded file.</span></span> 
    
  ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)
11. <span data-ttu-id="e9b3a-183">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-183">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>
    
   ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)
12. <span data-ttu-id="e9b3a-185">In the **Edit Federated Identity Provider User Settings** page perform the following actions and click **Save**.0</span><span class="sxs-lookup"><span data-stu-id="e9b3a-185">In the **Edit Federated Identity Provider User Settings** page perform the following actions and click **Save**.0</span></span>   
  1. <span data-ttu-id="e9b3a-186">Select **SAML NameID** as **Login name**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-186">Select **SAML NameID** as **Login name**.</span></span> 
  2. <span data-ttu-id="e9b3a-187">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: http://schemas.microsoft.com/identity/claims/displayname.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-187">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: http://schemas.microsoft.com/identity/claims/displayname.</span></span> 
  3. <span data-ttu-id="e9b3a-188">Select **Other** as **Email** and in the **Attribute name** textbox put the value: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-188">Select **Other** as **Email** and in the **Attribute name** textbox put the value: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress.</span></span> 
  4. <span data-ttu-id="e9b3a-189">Select **Yes** as **Auto-create account on signon**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-189">Select **Yes** as **Auto-create account on signon**.</span></span> 
  5. <span data-ttu-id="e9b3a-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-190">Click **Save** button.</span></span>
 
   ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
13. <span data-ttu-id="e9b3a-192">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-192">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]
14. <span data-ttu-id="e9b3a-194">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
   ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9b3a-196">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9b3a-196">Create an Azure AD test user</span></span>
<span data-ttu-id="e9b3a-197">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-197">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="e9b3a-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9b3a-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b3a-200">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-200">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="e9b3a-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9b3a-203">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="e9b3a-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="e9b3a-207">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="e9b3a-209">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-209">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="e9b3a-210">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-210">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="e9b3a-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-211">Click **Next**.</span></span>
6. <span data-ttu-id="e9b3a-212">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-212">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="e9b3a-214">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-214">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="e9b3a-215">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-215">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="e9b3a-216">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-216">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="e9b3a-217">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-217">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="e9b3a-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-218">Click **Next**.</span></span>
7. <span data-ttu-id="e9b3a-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="e9b3a-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9b3a-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="e9b3a-223">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-223">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="e9b3a-224">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-224">Click **Complete**.</span></span>   

### <a name="create-a-moveit-transfer-test-user"></a><span data-ttu-id="e9b3a-225">Create a MOVEit Transfer test user</span><span class="sxs-lookup"><span data-stu-id="e9b3a-225">Create a MOVEit Transfer test user</span></span>
<span data-ttu-id="e9b3a-226">The objective of this section is to create a user called Britta Simon in MOVEit Transfer.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-226">The objective of this section is to create a user called Britta Simon in MOVEit Transfer.</span></span> <span data-ttu-id="e9b3a-227">MOVEit Transfer supports just-in-time provisioning, which you have enabled.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-227">MOVEit Transfer supports just-in-time provisioning, which you have enabled.</span></span>

<span data-ttu-id="e9b3a-228">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-228">There is no action item for you in this section.</span></span> <span data-ttu-id="e9b3a-229">A new user will be created during an attempt to access MOVEit Transfer if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-229">A new user will be created during an attempt to access MOVEit Transfer if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e9b3a-230">If you need to create an user manually, you need to contact the MOVEit Transfer support team.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-230">If you need to create an user manually, you need to contact the MOVEit Transfer support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9b3a-231">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9b3a-231">Assign the Azure AD test user</span></span>
<span data-ttu-id="e9b3a-232">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to MOVEit Transfer.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-232">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to MOVEit Transfer.</span></span>

![Assign User][200]

<span data-ttu-id="e9b3a-234">**To assign Britta Simon to MOVEit Transfer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9b3a-234">**To assign Britta Simon to MOVEit Transfer, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b3a-235">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-235">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="e9b3a-237">In the applications list, select **MOVEit Transfer**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-237">In the applications list, select **MOVEit Transfer**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_50.png)
3. <span data-ttu-id="e9b3a-239">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-239">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="e9b3a-241">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-241">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e9b3a-242">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-242">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="e9b3a-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9b3a-244">Test single sign-on</span></span>
<span data-ttu-id="e9b3a-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-245">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e9b3a-246">When you click the MOVEit Transfer tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer application.</span><span class="sxs-lookup"><span data-stu-id="e9b3a-246">When you click the MOVEit Transfer tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9b3a-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9b3a-247">Additional resources</span></span>
* [<span data-ttu-id="e9b3a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9b3a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9b3a-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9b3a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moveittransfer-tutorial/tutorial_general_205.png

































