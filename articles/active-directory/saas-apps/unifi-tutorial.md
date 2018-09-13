---
title: 'Tutorial: Azure Active Directory integration with UNIFI | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and UNIFI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 35b1b9492b7bcd09c79cb5bd2509a6cfea205ae9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865595"
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="31dba-103">Tutorial: Azure Active Directory integration with UNIFI</span><span class="sxs-lookup"><span data-stu-id="31dba-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="31dba-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31dba-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31dba-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="31dba-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31dba-106">You can control in Azure AD who has access to UNIFI</span><span class="sxs-lookup"><span data-stu-id="31dba-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="31dba-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="31dba-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31dba-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="31dba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31dba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="31dba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31dba-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31dba-110">Prerequisites</span></span>

<span data-ttu-id="31dba-111">To configure Azure AD integration with UNIFI, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="31dba-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="31dba-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="31dba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31dba-113">A UNIFI single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="31dba-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31dba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="31dba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31dba-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="31dba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31dba-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="31dba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31dba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31dba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31dba-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="31dba-118">Scenario description</span></span>
<span data-ttu-id="31dba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="31dba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31dba-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="31dba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31dba-121">Adding UNIFI from the gallery</span><span class="sxs-lookup"><span data-stu-id="31dba-121">Adding UNIFI from the gallery</span></span>
1. <span data-ttu-id="31dba-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="31dba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="31dba-123">Adding UNIFI from the gallery</span><span class="sxs-lookup"><span data-stu-id="31dba-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="31dba-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="31dba-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31dba-125">**To add UNIFI from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="31dba-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31dba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="31dba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="31dba-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="31dba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31dba-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="31dba-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="31dba-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="31dba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="31dba-133">In the search box, type **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="31dba-133">In the search box, type **UNIFI**.</span></span>

    ![Creating an Azure AD test user](./media/unifi-tutorial/tutorial_unifi_search.png)

1. <span data-ttu-id="31dba-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="31dba-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31dba-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="31dba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31dba-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="31dba-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31dba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31dba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="31dba-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span><span class="sxs-lookup"><span data-stu-id="31dba-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="31dba-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="31dba-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31dba-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="31dba-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31dba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="31dba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="31dba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31dba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="31dba-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="31dba-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="31dba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="31dba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="31dba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="31dba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31dba-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="31dba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31dba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span><span class="sxs-lookup"><span data-stu-id="31dba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="31dba-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="31dba-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="31dba-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="31dba-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="31dba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="31dba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_samlbase.png)

1. <span data-ttu-id="31dba-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="31dba-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="31dba-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="31dba-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

1. <span data-ttu-id="31dba-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="31dba-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="31dba-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="31dba-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

1. <span data-ttu-id="31dba-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="31dba-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_certificate.png) 

1. <span data-ttu-id="31dba-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="31dba-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="31dba-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="31dba-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31dba-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="31dba-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_configure.png)

1. <span data-ttu-id="31dba-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="31dba-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

1. <span data-ttu-id="31dba-169">Click on the **Users**.</span><span class="sxs-lookup"><span data-stu-id="31dba-169">Click on the **Users**.</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/app1.png) 

1. <span data-ttu-id="31dba-171">Click on the **Add New Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="31dba-171">Click on the **Add New Identity Provider**.</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/app2.png)

1. <span data-ttu-id="31dba-173">In the **Add Identity Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="31dba-173">In the **Add Identity Provider** section, perform the following steps:</span></span>    

    ![Configure Single Sign-On](./media/unifi-tutorial/app3.png) 

    <span data-ttu-id="31dba-175">a.</span><span class="sxs-lookup"><span data-stu-id="31dba-175">a.</span></span> <span data-ttu-id="31dba-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span><span class="sxs-lookup"><span data-stu-id="31dba-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="31dba-177">b.</span><span class="sxs-lookup"><span data-stu-id="31dba-177">b.</span></span> <span data-ttu-id="31dba-178">In the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="31dba-178">In the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="31dba-179">c.</span><span class="sxs-lookup"><span data-stu-id="31dba-179">c.</span></span> <span data-ttu-id="31dba-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="31dba-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="31dba-181">d.</span><span class="sxs-lookup"><span data-stu-id="31dba-181">d.</span></span> <span data-ttu-id="31dba-182">Select the **is Default Provider** checkbox.</span><span class="sxs-lookup"><span data-stu-id="31dba-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="31dba-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="31dba-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31dba-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="31dba-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31dba-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31dba-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31dba-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="31dba-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="31dba-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31dba-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="31dba-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="31dba-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31dba-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="31dba-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/unifi-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="31dba-192">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="31dba-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/unifi-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="31dba-194">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="31dba-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/unifi-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="31dba-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="31dba-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31dba-198">a.</span><span class="sxs-lookup"><span data-stu-id="31dba-198">a.</span></span> <span data-ttu-id="31dba-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31dba-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31dba-200">b.</span><span class="sxs-lookup"><span data-stu-id="31dba-200">b.</span></span> <span data-ttu-id="31dba-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31dba-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31dba-202">c.</span><span class="sxs-lookup"><span data-stu-id="31dba-202">c.</span></span> <span data-ttu-id="31dba-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="31dba-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31dba-204">d.</span><span class="sxs-lookup"><span data-stu-id="31dba-204">d.</span></span> <span data-ttu-id="31dba-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="31dba-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="31dba-206">Creating a UNIFI test user</span><span class="sxs-lookup"><span data-stu-id="31dba-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="31dba-207">In this section, you create a user called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31dba-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="31dba-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span><span class="sxs-lookup"><span data-stu-id="31dba-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="31dba-209">Users are created automatically after successful authentication from the Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31dba-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31dba-210">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="31dba-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31dba-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span><span class="sxs-lookup"><span data-stu-id="31dba-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Assign User][200] 

<span data-ttu-id="31dba-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="31dba-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="31dba-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="31dba-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="31dba-216">In the applications list, select **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="31dba-216">In the applications list, select **UNIFI**.</span></span>

    ![Configure Single Sign-On](./media/unifi-tutorial/tutorial_unifi_app.png) 

1. <span data-ttu-id="31dba-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="31dba-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="31dba-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="31dba-220">Click **Add** button.</span></span> <span data-ttu-id="31dba-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="31dba-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="31dba-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="31dba-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="31dba-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="31dba-224">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="31dba-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="31dba-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31dba-226">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="31dba-226">Testing single sign-on</span></span>

<span data-ttu-id="31dba-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="31dba-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31dba-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span><span class="sxs-lookup"><span data-stu-id="31dba-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="31dba-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31dba-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="31dba-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="31dba-230">Additional resources</span></span>

* [<span data-ttu-id="31dba-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31dba-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="31dba-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31dba-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/unifi-tutorial/tutorial_general_01.png
[2]: ./media/unifi-tutorial/tutorial_general_02.png
[3]: ./media/unifi-tutorial/tutorial_general_03.png
[4]: ./media/unifi-tutorial/tutorial_general_04.png

[100]: ./media/unifi-tutorial/tutorial_general_100.png

[200]: ./media/unifi-tutorial/tutorial_general_200.png
[201]: ./media/unifi-tutorial/tutorial_general_201.png
[202]: ./media/unifi-tutorial/tutorial_general_202.png
[203]: ./media/unifi-tutorial/tutorial_general_203.png

