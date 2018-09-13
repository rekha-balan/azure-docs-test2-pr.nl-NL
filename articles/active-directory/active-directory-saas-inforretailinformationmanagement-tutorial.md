---
title: 'Tutorial: Azure Active Directory integration with Infor Retail – Information Management | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Infor Retail – Information Management.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 3bfc92fa5ace8aa5c190e194d27036b380620e5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550226"
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="44561-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="44561-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="44561-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44561-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44561-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="44561-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44561-106">You can control in Azure AD who has access to Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="44561-106">You can control in Azure AD who has access to Infor Retail – Information Management</span></span>
- <span data-ttu-id="44561-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="44561-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44561-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="44561-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="44561-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44561-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44561-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="44561-110">Prerequisites</span></span>

<span data-ttu-id="44561-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="44561-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span></span>

- <span data-ttu-id="44561-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="44561-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44561-113">An Infor Retail – Information Management single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="44561-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="44561-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="44561-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="44561-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="44561-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44561-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="44561-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="44561-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44561-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="44561-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="44561-118">Scenario description</span></span>
<span data-ttu-id="44561-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="44561-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44561-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="44561-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44561-121">Adding Infor Retail – Information Management from the gallery</span><span class="sxs-lookup"><span data-stu-id="44561-121">Adding Infor Retail – Information Management from the gallery</span></span>
2. <span data-ttu-id="44561-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="44561-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-infor-retail--information-management-from-the-gallery"></a><span data-ttu-id="44561-123">Adding Infor Retail – Information Management from the gallery</span><span class="sxs-lookup"><span data-stu-id="44561-123">Adding Infor Retail – Information Management from the gallery</span></span>
<span data-ttu-id="44561-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="44561-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44561-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44561-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44561-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="44561-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44561-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="44561-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44561-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="44561-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="44561-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="44561-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="44561-133">In the search box, type **Infor Retail – Information Management**.</span><span class="sxs-lookup"><span data-stu-id="44561-133">In the search box, type **Infor Retail – Information Management**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_001.png)

5. <span data-ttu-id="44561-135">In the results panel, select **Infor Retail – Information Management**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="44561-135">In the results panel, select **Infor Retail – Information Management**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44561-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="44561-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44561-138">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="44561-138">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44561-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44561-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span></span> <span data-ttu-id="44561-140">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span><span class="sxs-lookup"><span data-stu-id="44561-140">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span></span>

<span data-ttu-id="44561-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="44561-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Infor Retail – Information Management.</span></span>

<span data-ttu-id="44561-142">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="44561-142">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44561-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="44561-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44561-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44561-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44561-145">**[Creating an Infor Retail – Information Management test user](#creating-an-infor-retail---information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="44561-145">**[Creating an Infor Retail – Information Management test user](#creating-an-infor-retail---information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="44561-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="44561-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44561-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="44561-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44561-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="44561-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44561-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Infor Retail – Information Management application.</span><span class="sxs-lookup"><span data-stu-id="44561-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="44561-150">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44561-150">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="44561-151">In the Azure Management portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="44561-151">In the Azure Management portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="44561-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="44561-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_01.png)

3. <span data-ttu-id="44561-155">On the **Infor Retail – Information Management Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44561-155">On the **Infor Retail – Information Management Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_02.png)

    <span data-ttu-id="44561-157">a.</span><span class="sxs-lookup"><span data-stu-id="44561-157">a.</span></span> <span data-ttu-id="44561-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com`</span><span class="sxs-lookup"><span data-stu-id="44561-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com`</span></span>
    
    <span data-ttu-id="44561-159">b.</span><span class="sxs-lookup"><span data-stu-id="44561-159">b.</span></span> <span data-ttu-id="44561-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="44561-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>
    
4. <span data-ttu-id="44561-161">If you wish to configure the application in **SP initiated mode**, on the **Infor Retail – Information Management Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44561-161">If you wish to configure the application in **SP initiated mode**, on the **Infor Retail – Information Management Domain and URLs** section perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_03.png)

    <span data-ttu-id="44561-163">a.</span><span class="sxs-lookup"><span data-stu-id="44561-163">a.</span></span> <span data-ttu-id="44561-164">Click on the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="44561-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="44561-165">b.</span><span class="sxs-lookup"><span data-stu-id="44561-165">b.</span></span> <span data-ttu-id="44561-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="44561-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44561-167">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="44561-167">Please note that these are not the real values.</span></span> <span data-ttu-id="44561-168">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="44561-168">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="44561-169">Contact [Infor Retail – Information Management support team](mailto:innovate@infor.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="44561-169">Contact [Infor Retail – Information Management support team](mailto:innovate@infor.com) to get these values.</span></span>

5. <span data-ttu-id="44561-170">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="44561-170">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_04.png)  

6. <span data-ttu-id="44561-172">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="44561-172">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="44561-173">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="44561-173">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="44561-175">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="44561-175">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_05.png)

8. <span data-ttu-id="44561-177">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="44561-177">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="44561-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="44561-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_06.png) 

10. <span data-ttu-id="44561-181">To get SSO configured for your application, contact [Infor Retail – Information Management support team](mailto:innovate@infor.com) and provide them with the downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="44561-181">To get SSO configured for your application, contact [Infor Retail – Information Management support team](mailto:innovate@infor.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44561-182">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="44561-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="44561-183">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44561-183">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="44561-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44561-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44561-186">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="44561-186">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44561-188">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="44561-188">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44561-190">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="44561-190">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44561-192">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="44561-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44561-194">a.</span><span class="sxs-lookup"><span data-stu-id="44561-194">a.</span></span> <span data-ttu-id="44561-195">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44561-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44561-196">b.</span><span class="sxs-lookup"><span data-stu-id="44561-196">b.</span></span> <span data-ttu-id="44561-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44561-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44561-198">c.</span><span class="sxs-lookup"><span data-stu-id="44561-198">c.</span></span> <span data-ttu-id="44561-199">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="44561-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44561-200">d.</span><span class="sxs-lookup"><span data-stu-id="44561-200">d.</span></span> <span data-ttu-id="44561-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="44561-201">Click **Create**.</span></span> 



### <a name="creating-an-infor-retail--information-management-test-user"></a><span data-ttu-id="44561-202">Creating an Infor Retail – Information Management test user</span><span class="sxs-lookup"><span data-stu-id="44561-202">Creating an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="44561-203">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="44561-203">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="44561-204">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span><span class="sxs-lookup"><span data-stu-id="44561-204">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44561-205">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="44561-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44561-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="44561-206">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Infor Retail – Information Management.</span></span>

![Assign User][200] 

<span data-ttu-id="44561-208">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="44561-208">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="44561-209">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="44561-209">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="44561-211">In the applications list, select **Infor Retail – Information Management**.</span><span class="sxs-lookup"><span data-stu-id="44561-211">In the applications list, select **Infor Retail – Information Management**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_50.png) 

3. <span data-ttu-id="44561-213">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="44561-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="44561-215">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="44561-215">Click **Add** button.</span></span> <span data-ttu-id="44561-216">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="44561-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="44561-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="44561-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44561-219">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="44561-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44561-220">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="44561-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="44561-221">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="44561-221">Testing single sign-on</span></span>

<span data-ttu-id="44561-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="44561-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44561-223">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span><span class="sxs-lookup"><span data-stu-id="44561-223">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="44561-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="44561-224">Additional resources</span></span>

* [<span data-ttu-id="44561-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44561-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44561-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44561-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png























