---
title: 'Tutorial: Azure Active Directory integration with Evernote | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: jeedes
ms.openlocfilehash: 117d4718257bcd5a0149e34e02531ff1732df024
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552600"
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="77a9a-103">Tutorial: Azure Active Directory integration with Evernote</span><span class="sxs-lookup"><span data-stu-id="77a9a-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="77a9a-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77a9a-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77a9a-105">Integrating Evernote with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="77a9a-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77a9a-106">You can control in Azure AD who has access to Evernote</span><span class="sxs-lookup"><span data-stu-id="77a9a-106">You can control in Azure AD who has access to Evernote</span></span>
- <span data-ttu-id="77a9a-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="77a9a-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77a9a-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="77a9a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="77a9a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77a9a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77a9a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77a9a-110">Prerequisites</span></span>

<span data-ttu-id="77a9a-111">To configure Azure AD integration with Evernote, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="77a9a-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="77a9a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="77a9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77a9a-113">A Evernote single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="77a9a-113">A Evernote single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="77a9a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="77a9a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="77a9a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="77a9a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77a9a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="77a9a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="77a9a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77a9a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="77a9a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="77a9a-118">Scenario description</span></span>
<span data-ttu-id="77a9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="77a9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77a9a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="77a9a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77a9a-121">Adding Evernote from the gallery</span><span class="sxs-lookup"><span data-stu-id="77a9a-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="77a9a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="77a9a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="77a9a-123">Adding Evernote from the gallery</span><span class="sxs-lookup"><span data-stu-id="77a9a-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="77a9a-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="77a9a-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77a9a-125">**To add Evernote from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="77a9a-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77a9a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="77a9a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77a9a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77a9a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="77a9a-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="77a9a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="77a9a-133">In the search box, type **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-133">In the search box, type **Evernote**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_search01.png)

5. <span data-ttu-id="77a9a-135">In the results panel, select **Evernote**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="77a9a-135">In the results panel, select **Evernote**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_search_result01.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77a9a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="77a9a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77a9a-138">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77a9a-138">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77a9a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77a9a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="77a9a-140">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span><span class="sxs-lookup"><span data-stu-id="77a9a-140">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="77a9a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Evernote.</span><span class="sxs-lookup"><span data-stu-id="77a9a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Evernote.</span></span>

<span data-ttu-id="77a9a-142">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="77a9a-142">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77a9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="77a9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77a9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77a9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77a9a-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="77a9a-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="77a9a-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="77a9a-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77a9a-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="77a9a-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77a9a-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Evernote application.</span><span class="sxs-lookup"><span data-stu-id="77a9a-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="77a9a-149">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="77a9a-149">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="77a9a-150">In the Azure Management portal, on the **Evernote** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-150">In the Azure Management portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="77a9a-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="77a9a-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="77a9a-154">On the **Evernote Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span><span class="sxs-lookup"><span data-stu-id="77a9a-154">On the **Evernote Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_idp.png)
    
4. <span data-ttu-id="77a9a-156">On the **Evernote Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="77a9a-156">On the **Evernote Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_sp_01.png)
    
    <span data-ttu-id="77a9a-158">a.</span><span class="sxs-lookup"><span data-stu-id="77a9a-158">a.</span></span> <span data-ttu-id="77a9a-159">Click on the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="77a9a-159">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="77a9a-160">b.</span><span class="sxs-lookup"><span data-stu-id="77a9a-160">b.</span></span> <span data-ttu-id="77a9a-161">In the **Sign On URL** textbox, type the Sign-On URL : `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="77a9a-161">In the **Sign On URL** textbox, type the Sign-On URL : `https://www.evernote.com/Login.action`</span></span>

5. <span data-ttu-id="77a9a-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_cert.png)    

6. <span data-ttu-id="77a9a-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="77a9a-165">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="77a9a-165">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="77a9a-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="77a9a-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_makecertactive.png)

8. <span data-ttu-id="77a9a-169">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-169">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="77a9a-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="77a9a-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

10. <span data-ttu-id="77a9a-173">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="77a9a-173">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_configuresignon.png)

11. <span data-ttu-id="77a9a-176">In a different web browser window, log into your Evernote company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="77a9a-176">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

12. <span data-ttu-id="77a9a-177">Go to **'Admin Console'**</span><span class="sxs-lookup"><span data-stu-id="77a9a-177">Go to **'Admin Console'**</span></span>

    ![Admin-Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

13. <span data-ttu-id="77a9a-179">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span><span class="sxs-lookup"><span data-stu-id="77a9a-179">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

14. <span data-ttu-id="77a9a-181">Configure the following values:</span><span class="sxs-lookup"><span data-stu-id="77a9a-181">Configure the following values:</span></span>

    <span data-ttu-id="77a9a-182">a.</span><span class="sxs-lookup"><span data-stu-id="77a9a-182">a.</span></span>  <span data-ttu-id="77a9a-183">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span><span class="sxs-lookup"><span data-stu-id="77a9a-183">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="77a9a-184">b.</span><span class="sxs-lookup"><span data-stu-id="77a9a-184">b.</span></span> <span data-ttu-id="77a9a-185">**SAML HTTP Request URL** - Enter **SAML Single sign-on Service URL** from the **Configure Evernote** section on Azure AD</span><span class="sxs-lookup"><span data-stu-id="77a9a-185">**SAML HTTP Request URL** - Enter **SAML Single sign-on Service URL** from the **Configure Evernote** section on Azure AD</span></span>

    <span data-ttu-id="77a9a-186">c.</span><span class="sxs-lookup"><span data-stu-id="77a9a-186">c.</span></span> <span data-ttu-id="77a9a-187">**X.509 Certificate** - Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="77a9a-187">**X.509 Certificate** - Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Certificate-Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)

    <span data-ttu-id="77a9a-189">d.Click **Save Changes**</span><span class="sxs-lookup"><span data-stu-id="77a9a-189">d.Click **Save Changes**</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77a9a-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="77a9a-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="77a9a-191">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77a9a-191">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="77a9a-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="77a9a-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77a9a-194">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="77a9a-194">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77a9a-196">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="77a9a-196">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77a9a-198">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="77a9a-198">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77a9a-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="77a9a-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77a9a-202">a.</span><span class="sxs-lookup"><span data-stu-id="77a9a-202">a.</span></span> <span data-ttu-id="77a9a-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77a9a-204">b.</span><span class="sxs-lookup"><span data-stu-id="77a9a-204">b.</span></span> <span data-ttu-id="77a9a-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77a9a-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77a9a-206">c.</span><span class="sxs-lookup"><span data-stu-id="77a9a-206">c.</span></span> <span data-ttu-id="77a9a-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77a9a-208">d.</span><span class="sxs-lookup"><span data-stu-id="77a9a-208">d.</span></span> <span data-ttu-id="77a9a-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-209">Click **Create**.</span></span> 



### <a name="creating-an-evernote-test-user"></a><span data-ttu-id="77a9a-210">Creating an Evernote test user</span><span class="sxs-lookup"><span data-stu-id="77a9a-210">Creating an Evernote test user</span></span>

<span data-ttu-id="77a9a-211">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span><span class="sxs-lookup"><span data-stu-id="77a9a-211">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="77a9a-212">In the case of Evernote, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="77a9a-212">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="77a9a-213">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="77a9a-213">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="77a9a-214">Log in to your Evernote company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="77a9a-214">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="77a9a-215">Click the **'Admin Console'**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-215">Click the **'Admin Console'**.</span></span>

    ![Admin-Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="77a9a-217">From the **'Admin Console'**, go to **‘Add users’**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-217">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Add-testUser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="77a9a-219">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span><span class="sxs-lookup"><span data-stu-id="77a9a-219">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Add-testUser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="77a9a-221">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span><span class="sxs-lookup"><span data-stu-id="77a9a-221">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77a9a-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="77a9a-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77a9a-223">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Evernote.</span><span class="sxs-lookup"><span data-stu-id="77a9a-223">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Evernote.</span></span>

![Assign User][200] 

<span data-ttu-id="77a9a-225">**To assign Britta Simon to Evernote, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="77a9a-225">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="77a9a-226">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-226">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="77a9a-228">In the applications list, select **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-228">In the applications list, select **Evernote**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png) 

3. <span data-ttu-id="77a9a-230">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="77a9a-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="77a9a-232">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="77a9a-232">Click **Add** button.</span></span> <span data-ttu-id="77a9a-233">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="77a9a-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="77a9a-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="77a9a-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77a9a-236">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="77a9a-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77a9a-237">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="77a9a-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="77a9a-238">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="77a9a-238">Testing single sign-on</span></span>

<span data-ttu-id="77a9a-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="77a9a-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="77a9a-240">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span><span class="sxs-lookup"><span data-stu-id="77a9a-240">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="77a9a-241">You'll be logging in as an Organization account but then need to log in with your personal account.</span><span class="sxs-lookup"><span data-stu-id="77a9a-241">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="77a9a-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="77a9a-242">Additional resources</span></span>

* [<span data-ttu-id="77a9a-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77a9a-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77a9a-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77a9a-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-evernote-tutorial/tutorial_general_203.png
































