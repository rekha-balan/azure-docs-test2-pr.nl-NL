---
title: 'Tutorial: Azure Active Directory integration with T&E Express | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and T&E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 20e8ef80787785825d7513deccab11fdd7ce5647
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662659"
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="34099-103">Tutorial: Azure Active Directory integration with T&E Express</span><span class="sxs-lookup"><span data-stu-id="34099-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="34099-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34099-104">In this tutorial, you learn how to integrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34099-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="34099-105">Integrating T&E Express with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34099-106">You can control in Azure AD who has access to T&E Express</span><span class="sxs-lookup"><span data-stu-id="34099-106">You can control in Azure AD who has access to T&E Express</span></span>
- <span data-ttu-id="34099-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="34099-107">You can enable your users to automatically get signed-on to T&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34099-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="34099-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="34099-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34099-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34099-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="34099-110">Prerequisites</span></span>

<span data-ttu-id="34099-111">To configure Azure AD integration with T&E Express, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="34099-111">To configure Azure AD integration with T&E Express, you need the following items:</span></span>

- <span data-ttu-id="34099-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="34099-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34099-113">A T&E Express single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="34099-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34099-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="34099-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34099-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="34099-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34099-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="34099-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="34099-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34099-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34099-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="34099-118">Scenario description</span></span>
<span data-ttu-id="34099-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="34099-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34099-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="34099-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34099-121">Adding T&E Express from the gallery</span><span class="sxs-lookup"><span data-stu-id="34099-121">Adding T&E Express from the gallery</span></span>
2. <span data-ttu-id="34099-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34099-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-the-gallery"></a><span data-ttu-id="34099-123">Adding T&E Express from the gallery</span><span class="sxs-lookup"><span data-stu-id="34099-123">Adding T&E Express from the gallery</span></span>
<span data-ttu-id="34099-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="34099-124">To configure the integration of T&E Express into Azure AD, you need to add T&E Express from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34099-125">**To add T&E Express from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34099-125">**To add T&E Express from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34099-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="34099-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34099-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="34099-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34099-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="34099-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="34099-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="34099-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="34099-133">In the search box, type **T&E Express**.</span><span class="sxs-lookup"><span data-stu-id="34099-133">In the search box, type **T&E Express**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="34099-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="34099-135">In the results panel, select **T&E Express**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34099-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34099-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34099-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="34099-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34099-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34099-139">For single sign-on to work, Azure AD needs to know what the counterpart user in T&E Express is to a user in Azure AD.</span></span> <span data-ttu-id="34099-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span><span class="sxs-lookup"><span data-stu-id="34099-140">In other words, a link relationship between an Azure AD user and the related user in T&E Express needs to be established.</span></span>

<span data-ttu-id="34099-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span><span class="sxs-lookup"><span data-stu-id="34099-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in T&E Express.</span></span>

<span data-ttu-id="34099-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="34099-142">To configure and test Azure AD single sign-on with T&E Express, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34099-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="34099-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="34099-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34099-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34099-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="34099-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - to have a counterpart of Britta Simon in T&E Express that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="34099-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="34099-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34099-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="34099-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34099-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34099-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34099-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span><span class="sxs-lookup"><span data-stu-id="34099-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="34099-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34099-150">**To configure Azure AD single sign-on with T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="34099-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="34099-151">In the Azure Management portal, on the **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="34099-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="34099-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="34099-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="34099-155">On the **T&E Express Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="34099-157">a.</span><span class="sxs-lookup"><span data-stu-id="34099-157">a.</span></span> <span data-ttu-id="34099-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="34099-158">In the **Identifier** textbox, type the value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="34099-159">b.</span><span class="sxs-lookup"><span data-stu-id="34099-159">b.</span></span> <span data-ttu-id="34099-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="34099-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34099-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="34099-161">Please note that these are not the real values.</span></span> <span data-ttu-id="34099-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="34099-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="34099-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="34099-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="34099-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span><span class="sxs-lookup"><span data-stu-id="34099-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) to get these values.</span></span>

5. <span data-ttu-id="34099-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="34099-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="34099-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="34099-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="34099-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="34099-169">To configure single sign-on on **T&E Express** side, login to the T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="34099-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span><span class="sxs-lookup"><span data-stu-id="34099-170">Under the **Admin** Tab, Click on **SAML domain** to Open the SAML settings page.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tye-saml.png)

10. <span data-ttu-id="34099-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="34099-172">Select the **Activar(Activate)** option from **No** to **SI(Yes)**.</span></span> <span data-ttu-id="34099-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="34099-173">In the **Identity Provider Metadata** textbox, paste the metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tyeadmin.png)

11. <span data-ttu-id="34099-175">Click on the **Guardar(Save)** button to save the settings.</span><span class="sxs-lookup"><span data-stu-id="34099-175">Click on the **Guardar(Save)** button to save the settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34099-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="34099-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="34099-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34099-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="34099-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34099-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34099-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="34099-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34099-182">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="34099-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34099-184">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="34099-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34099-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="34099-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34099-188">a.</span><span class="sxs-lookup"><span data-stu-id="34099-188">a.</span></span> <span data-ttu-id="34099-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34099-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34099-190">b.</span><span class="sxs-lookup"><span data-stu-id="34099-190">b.</span></span> <span data-ttu-id="34099-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34099-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34099-192">c.</span><span class="sxs-lookup"><span data-stu-id="34099-192">c.</span></span> <span data-ttu-id="34099-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="34099-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="34099-194">d.</span><span class="sxs-lookup"><span data-stu-id="34099-194">d.</span></span> <span data-ttu-id="34099-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="34099-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="34099-196">Creating a T&E Express test user</span><span class="sxs-lookup"><span data-stu-id="34099-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="34099-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span><span class="sxs-lookup"><span data-stu-id="34099-197">In order to enable Azure AD users to log into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="34099-198">In case of T&E Express, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="34099-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="34099-199">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34099-199">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="34099-200">Log in to your T&E Express company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="34099-200">Log in to your T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="34099-201">Under Admin tag, click on Users to open the Users master page.</span><span class="sxs-lookup"><span data-stu-id="34099-201">Under Admin tag, click on Users to open the Users master page.</span></span>

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="34099-203">On the home page, click on **+** to add the users.</span><span class="sxs-lookup"><span data-stu-id="34099-203">On the home page, click on **+** to add the users.</span></span>

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="34099-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span><span class="sxs-lookup"><span data-stu-id="34099-205">Enter all the mandatory details as asked in the form and click the save button to save the details.</span></span>

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Add Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="34099-208">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="34099-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="34099-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span><span class="sxs-lookup"><span data-stu-id="34099-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to T&E Express.</span></span>

![Assign User][200] 

<span data-ttu-id="34099-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34099-211">**To assign Britta Simon to T&E Express, perform the following steps:**</span></span>

1. <span data-ttu-id="34099-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="34099-212">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="34099-214">In the applications list, select **T&E Express**.</span><span class="sxs-lookup"><span data-stu-id="34099-214">In the applications list, select **T&E Express**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="34099-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="34099-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="34099-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="34099-218">Click **Add** button.</span></span> <span data-ttu-id="34099-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="34099-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="34099-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="34099-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="34099-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="34099-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34099-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="34099-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34099-224">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="34099-224">Testing single sign-on</span></span>

<span data-ttu-id="34099-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="34099-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="34099-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span><span class="sxs-lookup"><span data-stu-id="34099-226">When you click the T&E Express tile in the Access Panel, you should get automatically signed-on to your T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34099-227">Additional resources</span><span class="sxs-lookup"><span data-stu-id="34099-227">Additional resources</span></span>

* [<span data-ttu-id="34099-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34099-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34099-229">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34099-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png



























