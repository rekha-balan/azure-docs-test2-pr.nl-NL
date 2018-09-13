---
title: 'Tutorial: Azure Active Directory integration with Wingspan eTMF | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Wingspan eTMF.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: d27d2c6a6c6bae2ebd13f78da308f32275993ec5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871334"
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="f79d2-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="f79d2-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="f79d2-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f79d2-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f79d2-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f79d2-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f79d2-106">You can control in Azure AD who has access to Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="f79d2-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="f79d2-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f79d2-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f79d2-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f79d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f79d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f79d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f79d2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f79d2-110">Prerequisites</span></span>

<span data-ttu-id="f79d2-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f79d2-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="f79d2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f79d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f79d2-113">A Wingspan eTMF single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f79d2-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f79d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f79d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f79d2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f79d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f79d2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f79d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f79d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f79d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f79d2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f79d2-118">Scenario description</span></span>
<span data-ttu-id="f79d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f79d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f79d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f79d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f79d2-121">Adding Wingspan eTMF from the gallery</span><span class="sxs-lookup"><span data-stu-id="f79d2-121">Adding Wingspan eTMF from the gallery</span></span>
1. <span data-ttu-id="f79d2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f79d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="f79d2-123">Adding Wingspan eTMF from the gallery</span><span class="sxs-lookup"><span data-stu-id="f79d2-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="f79d2-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f79d2-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f79d2-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f79d2-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f79d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f79d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f79d2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f79d2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f79d2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f79d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f79d2-133">In the search box, type **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

1. <span data-ttu-id="f79d2-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f79d2-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f79d2-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f79d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f79d2-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f79d2-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f79d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f79d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="f79d2-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f79d2-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="f79d2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f79d2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="f79d2-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f79d2-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f79d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f79d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f79d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f79d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f79d2-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f79d2-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f79d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f79d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f79d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f79d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f79d2-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f79d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f79d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span><span class="sxs-lookup"><span data-stu-id="f79d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="f79d2-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f79d2-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="f79d2-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f79d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f79d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

1. <span data-ttu-id="f79d2-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f79d2-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="f79d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="f79d2-157">a.</span></span> <span data-ttu-id="f79d2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="f79d2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="f79d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f79d2-159">b.</span></span> <span data-ttu-id="f79d2-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="f79d2-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="f79d2-161">c.</span><span class="sxs-lookup"><span data-stu-id="f79d2-161">c.</span></span> <span data-ttu-id="f79d2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="f79d2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="f79d2-163">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="f79d2-163">These values are not the real.</span></span> <span data-ttu-id="f79d2-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span><span class="sxs-lookup"><span data-stu-id="f79d2-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="f79d2-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f79d2-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

1. <span data-ttu-id="f79d2-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f79d2-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

1. <span data-ttu-id="f79d2-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f79d2-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/wingspanetmf-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f79d2-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="f79d2-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="f79d2-171">They set this up to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f79d2-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f79d2-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f79d2-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f79d2-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f79d2-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f79d2-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f79d2-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f79d2-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f79d2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="f79d2-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f79d2-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f79d2-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f79d2-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f79d2-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f79d2-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f79d2-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f79d2-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f79d2-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f79d2-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f79d2-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f79d2-187">a.</span><span class="sxs-lookup"><span data-stu-id="f79d2-187">a.</span></span> <span data-ttu-id="f79d2-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f79d2-189">b.</span><span class="sxs-lookup"><span data-stu-id="f79d2-189">b.</span></span> <span data-ttu-id="f79d2-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f79d2-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f79d2-191">c.</span><span class="sxs-lookup"><span data-stu-id="f79d2-191">c.</span></span> <span data-ttu-id="f79d2-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f79d2-193">d.</span><span class="sxs-lookup"><span data-stu-id="f79d2-193">d.</span></span> <span data-ttu-id="f79d2-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="f79d2-195">Creating a Wingspan eTMF test user</span><span class="sxs-lookup"><span data-stu-id="f79d2-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="f79d2-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f79d2-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="f79d2-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span><span class="sxs-lookup"><span data-stu-id="f79d2-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="f79d2-198">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f79d2-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f79d2-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f79d2-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f79d2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="f79d2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Assign User][200] 

<span data-ttu-id="f79d2-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f79d2-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="f79d2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f79d2-205">In the applications list, select **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Configure Single Sign-On](./media/wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

1. <span data-ttu-id="f79d2-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f79d2-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f79d2-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f79d2-209">Click **Add** button.</span></span> <span data-ttu-id="f79d2-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f79d2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f79d2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f79d2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f79d2-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f79d2-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f79d2-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f79d2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f79d2-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f79d2-215">Testing single sign-on</span></span>

<span data-ttu-id="f79d2-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f79d2-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="f79d2-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span><span class="sxs-lookup"><span data-stu-id="f79d2-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="f79d2-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span><span class="sxs-lookup"><span data-stu-id="f79d2-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="f79d2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f79d2-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f79d2-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f79d2-220">Additional resources</span></span>

* [<span data-ttu-id="f79d2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f79d2-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f79d2-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f79d2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/wingspanetmf-tutorial/tutorial_general_203.png

