---
title: 'Tutorial: Azure Active Directory integration with EasyTerritory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EasyTerritory.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 0974ab08e4e63c3f675f8b0ce83cf1a1c504fe5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548956"
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="104ff-103">Tutorial: Azure Active Directory integration with EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="104ff-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="104ff-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="104ff-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="104ff-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="104ff-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="104ff-106">You can control in Azure AD who has access to EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="104ff-106">You can control in Azure AD who has access to EasyTerritory</span></span>
- <span data-ttu-id="104ff-107">You can enable your users to automatically get signed-on to EasyTerritory single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="104ff-107">You can enable your users to automatically get signed-on to EasyTerritory single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="104ff-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="104ff-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="104ff-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="104ff-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="104ff-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="104ff-110">Prerequisites</span></span>

<span data-ttu-id="104ff-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="104ff-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="104ff-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="104ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="104ff-113">An EasyTerritory single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="104ff-113">An EasyTerritory single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="104ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="104ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="104ff-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="104ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="104ff-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="104ff-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="104ff-117">If you don't have an Azure AD trial environment, you can get trial [an one-month](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="104ff-117">If you don't have an Azure AD trial environment, you can get trial [an one-month](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="104ff-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="104ff-118">Scenario description</span></span>
<span data-ttu-id="104ff-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="104ff-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="104ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="104ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="104ff-121">Adding EasyTerritory from the gallery</span><span class="sxs-lookup"><span data-stu-id="104ff-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="104ff-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="104ff-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="104ff-123">Adding EasyTerritory from the gallery</span><span class="sxs-lookup"><span data-stu-id="104ff-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="104ff-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="104ff-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="104ff-125">**To add EasyTerritory from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="104ff-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="104ff-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="104ff-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="104ff-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="104ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="104ff-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="104ff-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="104ff-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="104ff-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="104ff-133">In the search box, type **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="104ff-133">In the search box, type **EasyTerritory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_001.png)

5. <span data-ttu-id="104ff-135">In the results panel, select **EasyTerritory**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="104ff-135">In the results panel, select **EasyTerritory**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="104ff-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="104ff-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="104ff-138">In this section, you configure and test Azure AD SSO with EasyTerritory based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="104ff-138">In this section, you configure and test Azure AD SSO with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="104ff-139">For SSO to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="104ff-139">For SSO to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="104ff-140">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span><span class="sxs-lookup"><span data-stu-id="104ff-140">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="104ff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="104ff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in EasyTerritory.</span></span>

<span data-ttu-id="104ff-142">To configure and test Azure AD SSO with EasyTerritory, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="104ff-142">To configure and test Azure AD SSO with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="104ff-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="104ff-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="104ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="104ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="104ff-145">**[Creating an EasyTerritory test user](#creating-an-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="104ff-145">**[Creating an EasyTerritory test user](#creating-an-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="104ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="104ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="104ff-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="104ff-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="104ff-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="104ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="104ff-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure SSO in your EasyTerritory application.</span><span class="sxs-lookup"><span data-stu-id="104ff-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure SSO in your EasyTerritory application.</span></span>

<span data-ttu-id="104ff-150">**To configure Azure AD SSO with EasyTerritory, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="104ff-150">**To configure Azure AD SSO with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="104ff-151">In the Azure Management portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="104ff-151">In the Azure Management portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="104ff-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable SSO.</span><span class="sxs-lookup"><span data-stu-id="104ff-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_01.png)

3. <span data-ttu-id="104ff-155">On the **EasyTerritory Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="104ff-155">On the **EasyTerritory Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_02.png)
   1. <span data-ttu-id="104ff-157">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/`</span><span class="sxs-lookup"><span data-stu-id="104ff-157">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/`</span></span>
   2. <span data-ttu-id="104ff-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/AuthServices/Acs`</span><span class="sxs-lookup"><span data-stu-id="104ff-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/AuthServices/Acs`</span></span>
    
4. <span data-ttu-id="104ff-159">If you wish to configure the application in **SP initiated mode**, on the **EasyTerritory Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="104ff-159">If you wish to configure the application in **SP initiated mode**, on the **EasyTerritory Domain and URLs** section perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_03.png)
  1. <span data-ttu-id="104ff-161">Click on the **Show advanced URL settings** option.</span><span class="sxs-lookup"><span data-stu-id="104ff-161">Click on the **Show advanced URL settings** option.</span></span>
  2. <span data-ttu-id="104ff-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="104ff-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>

    >[!NOTE] 
    ><span data-ttu-id="104ff-163">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="104ff-163">These are not the real values.</span></span> <span data-ttu-id="104ff-164">You have to update these values with the actual Sign On URL, Identifier and Reply URL.Contact [EasyTerritory support team](mailto:sales@easyterritory.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="104ff-164">You have to update these values with the actual Sign On URL, Identifier and Reply URL.Contact [EasyTerritory support team](mailto:sales@easyterritory.com) to get these values.</span></span>

5. <span data-ttu-id="104ff-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="104ff-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_04.png)    

6. <span data-ttu-id="104ff-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="104ff-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="104ff-168">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="104ff-168">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="104ff-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="104ff-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_05.png)

8. <span data-ttu-id="104ff-172">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="104ff-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="104ff-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="104ff-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_06.png) 

10. <span data-ttu-id="104ff-176">To get SSO configured for your application, contact [EasyTerritory support team](mailto:sales@easyterritory.com) and provide them with downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="104ff-176">To get SSO configured for your application, contact [EasyTerritory support team](mailto:sales@easyterritory.com) and provide them with downloaded **metadata**.</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="104ff-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="104ff-177">Create an Azure AD test user</span></span>
<span data-ttu-id="104ff-178">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="104ff-178">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="104ff-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="104ff-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="104ff-181">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="104ff-181">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="104ff-183">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="104ff-183">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="104ff-185">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="104ff-185">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="104ff-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="104ff-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png) 
 1. <span data-ttu-id="104ff-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="104ff-189">In the **Name** textbox, type **BrittaSimon**.</span></span>
 2. <span data-ttu-id="104ff-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="104ff-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
 3. <span data-ttu-id="104ff-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="104ff-191">Select **Show Password** and write down the value of the **Password**.</span></span>
 4. <span data-ttu-id="104ff-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="104ff-192">Click **Create**.</span></span> 

### <a name="create-an-easyterritory-test-user"></a><span data-ttu-id="104ff-193">Create an EasyTerritory test user</span><span class="sxs-lookup"><span data-stu-id="104ff-193">Create an EasyTerritory test user</span></span>

<span data-ttu-id="104ff-194">In this section, you create a user called Britta Simon in EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="104ff-194">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="104ff-195">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span><span class="sxs-lookup"><span data-stu-id="104ff-195">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="104ff-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="104ff-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="104ff-197">In this section, you enable Britta Simon to use Azure SSO by granting her access to EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="104ff-197">In this section, you enable Britta Simon to use Azure SSO by granting her access to EasyTerritory.</span></span>

![Assign User][200] 

<span data-ttu-id="104ff-199">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="104ff-199">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="104ff-200">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="104ff-200">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="104ff-202">In the applications list, select **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="104ff-202">In the applications list, select **EasyTerritory**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_50.png) 

3. <span data-ttu-id="104ff-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="104ff-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="104ff-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="104ff-206">Click **Add** button.</span></span> <span data-ttu-id="104ff-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="104ff-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="104ff-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="104ff-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="104ff-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="104ff-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="104ff-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="104ff-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="104ff-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="104ff-212">Testing single sign-on</span></span>

<span data-ttu-id="104ff-213">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="104ff-213">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="104ff-214">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span><span class="sxs-lookup"><span data-stu-id="104ff-214">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="104ff-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="104ff-215">Additional resources</span></span>

* [<span data-ttu-id="104ff-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="104ff-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="104ff-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="104ff-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png























