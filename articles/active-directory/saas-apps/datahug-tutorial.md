---
title: 'Tutorial: Azure Active Directory integration with Datahug | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: b3c67d794bd5947dc377cbdb7578e23ff3e05390
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871252"
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="e1a0a-103">Tutorial: Azure Active Directory integration with Datahug</span><span class="sxs-lookup"><span data-stu-id="e1a0a-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="e1a0a-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1a0a-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1a0a-105">Integrating Datahug with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1a0a-106">You can control in Azure AD who has access to Datahug</span><span class="sxs-lookup"><span data-stu-id="e1a0a-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="e1a0a-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e1a0a-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1a0a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1a0a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1a0a-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e1a0a-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e1a0a-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1a0a-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1a0a-111">Prerequisites</span></span>

<span data-ttu-id="e1a0a-112">To configure Azure AD integration with Datahug, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="e1a0a-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e1a0a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e1a0a-114">A Datahug single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e1a0a-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1a0a-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1a0a-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1a0a-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1a0a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1a0a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1a0a-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e1a0a-119">Scenario description</span></span>
<span data-ttu-id="e1a0a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1a0a-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1a0a-122">Adding Datahug from the gallery</span><span class="sxs-lookup"><span data-stu-id="e1a0a-122">Adding Datahug from the gallery</span></span>
1. <span data-ttu-id="e1a0a-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1a0a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="e1a0a-124">Adding Datahug from the gallery</span><span class="sxs-lookup"><span data-stu-id="e1a0a-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="e1a0a-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1a0a-126">**To add Datahug from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1a0a-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="e1a0a-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1a0a-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="e1a0a-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="e1a0a-134">In the search box, type **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-134">In the search box, type **Datahug**.</span></span>

    ![Creating an Azure AD test user](./media/datahug-tutorial/tutorial_datahug_search.png)

1. <span data-ttu-id="e1a0a-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1a0a-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1a0a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1a0a-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e1a0a-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1a0a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="e1a0a-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="e1a0a-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="e1a0a-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1a0a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e1a0a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e1a0a-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e1a0a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e1a0a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1a0a-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1a0a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1a0a-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="e1a0a-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="e1a0a-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="e1a0a-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_samlbase.png)

1. <span data-ttu-id="e1a0a-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="e1a0a-158">a.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-158">a.</span></span> <span data-ttu-id="e1a0a-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="e1a0a-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="e1a0a-160">b.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-160">b.</span></span> <span data-ttu-id="e1a0a-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="e1a0a-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

1. <span data-ttu-id="e1a0a-162">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="e1a0a-163">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="e1a0a-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="e1a0a-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e1a0a-166">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-166">These values are not the real.</span></span> <span data-ttu-id="e1a0a-167">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e1a0a-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="e1a0a-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

1. <span data-ttu-id="e1a0a-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_certificate.png) 

1.  <span data-ttu-id="e1a0a-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="e1a0a-174">a.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-174">a.</span></span> <span data-ttu-id="e1a0a-175">In **Signing Option**, select **Sign SAML assertion**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="e1a0a-176">b.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-176">b.</span></span> <span data-ttu-id="e1a0a-177">In **Signing algorithm**, select **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
1. <span data-ttu-id="e1a0a-178">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-178">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="e1a0a-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e1a0a-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_configure.png) 

1. <span data-ttu-id="e1a0a-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="e1a0a-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="e1a0a-184">They set this application up to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e1a0a-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e1a0a-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1a0a-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1a0a-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1a0a-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1a0a-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e1a0a-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1a0a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="e1a0a-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1a0a-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/datahug-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e1a0a-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/datahug-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="e1a0a-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/datahug-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e1a0a-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1a0a-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1a0a-200">a.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-200">a.</span></span> <span data-ttu-id="e1a0a-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1a0a-202">b.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-202">b.</span></span> <span data-ttu-id="e1a0a-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1a0a-204">c.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-204">c.</span></span> <span data-ttu-id="e1a0a-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1a0a-206">d.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-206">d.</span></span> <span data-ttu-id="e1a0a-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="e1a0a-208">Creating a Datahug test user</span><span class="sxs-lookup"><span data-stu-id="e1a0a-208">Creating a Datahug test user</span></span>

<span data-ttu-id="e1a0a-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="e1a0a-210">When Datahug, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="e1a0a-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e1a0a-212">Log in to your Datahug company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-212">Log in to your Datahug company site as an administrator.</span></span>

1. <span data-ttu-id="e1a0a-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Add Employee](./media/datahug-tutorial/1.png)

1. <span data-ttu-id="e1a0a-215">Choose **People** and click the **Add Users** tab</span><span class="sxs-lookup"><span data-stu-id="e1a0a-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Add Employee](./media/datahug-tutorial/2.png)

1. <span data-ttu-id="e1a0a-217">Type the email of the person you would like to create an account for and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Add Employee](./media/datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="e1a0a-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="e1a0a-220">If you are creating an account for Salesforce do not send the welcome email.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e1a0a-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e1a0a-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e1a0a-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Assign User][200] 

<span data-ttu-id="e1a0a-224">**To assign Britta Simon to Datahug, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e1a0a-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="e1a0a-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e1a0a-227">In the applications list, select **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-227">In the applications list, select **Datahug**.</span></span>

    ![Configure Single Sign-On](./media/datahug-tutorial/tutorial_datahug_app.png) 

1. <span data-ttu-id="e1a0a-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="e1a0a-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-231">Click **Add** button.</span></span> <span data-ttu-id="e1a0a-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="e1a0a-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e1a0a-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e1a0a-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1a0a-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e1a0a-237">Testing single sign-on</span></span>

<span data-ttu-id="e1a0a-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="e1a0a-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span><span class="sxs-lookup"><span data-stu-id="e1a0a-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="e1a0a-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1a0a-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e1a0a-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e1a0a-241">Additional resources</span></span>

* [<span data-ttu-id="e1a0a-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1a0a-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e1a0a-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1a0a-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/datahug-tutorial/tutorial_general_01.png
[2]: ./media/datahug-tutorial/tutorial_general_02.png
[3]: ./media/datahug-tutorial/tutorial_general_03.png
[4]: ./media/datahug-tutorial/tutorial_general_04.png

[100]: ./media/datahug-tutorial/tutorial_general_100.png

[200]: ./media/datahug-tutorial/tutorial_general_200.png
[201]: ./media/datahug-tutorial/tutorial_general_201.png
[202]: ./media/datahug-tutorial/tutorial_general_202.png
[203]: ./media/datahug-tutorial/tutorial_general_203.png

