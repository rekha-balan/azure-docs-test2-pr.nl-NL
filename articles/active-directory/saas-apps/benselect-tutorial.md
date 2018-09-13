---
title: 'Tutorial: Azure Active Directory integration with BenSelect | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BenSelect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 9af2de667085ef736c3ae37b75e3c67981161267
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868863"
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="78c41-103">Tutorial: Azure Active Directory integration with BenSelect</span><span class="sxs-lookup"><span data-stu-id="78c41-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="78c41-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78c41-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78c41-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="78c41-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78c41-106">You can control in Azure AD who has access to BenSelect</span><span class="sxs-lookup"><span data-stu-id="78c41-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="78c41-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="78c41-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78c41-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="78c41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78c41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="78c41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78c41-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="78c41-110">Prerequisites</span></span>

<span data-ttu-id="78c41-111">To configure Azure AD integration with BenSelect, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="78c41-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="78c41-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="78c41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78c41-113">A BenSelect single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="78c41-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78c41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="78c41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78c41-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="78c41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78c41-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="78c41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78c41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78c41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78c41-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="78c41-118">Scenario description</span></span>
<span data-ttu-id="78c41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="78c41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78c41-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="78c41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78c41-121">Adding BenSelect from the gallery</span><span class="sxs-lookup"><span data-stu-id="78c41-121">Adding BenSelect from the gallery</span></span>
1. <span data-ttu-id="78c41-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="78c41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="78c41-123">Adding BenSelect from the gallery</span><span class="sxs-lookup"><span data-stu-id="78c41-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="78c41-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="78c41-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78c41-125">**To add BenSelect from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="78c41-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78c41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="78c41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="78c41-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="78c41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78c41-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="78c41-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="78c41-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="78c41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="78c41-133">In the search box, type **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="78c41-133">In the search box, type **BenSelect**.</span></span>

    ![Creating an Azure AD test user](./media/benselect-tutorial/tutorial_benselect_search.png)

1. <span data-ttu-id="78c41-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="78c41-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78c41-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="78c41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78c41-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="78c41-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78c41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78c41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="78c41-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span><span class="sxs-lookup"><span data-stu-id="78c41-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="78c41-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="78c41-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78c41-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="78c41-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78c41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="78c41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="78c41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78c41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="78c41-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="78c41-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="78c41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="78c41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="78c41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="78c41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78c41-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="78c41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78c41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span><span class="sxs-lookup"><span data-stu-id="78c41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="78c41-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="78c41-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="78c41-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="78c41-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="78c41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="78c41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_samlbase.png)

1. <span data-ttu-id="78c41-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="78c41-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="78c41-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="78c41-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78c41-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="78c41-158">This value is not real.</span></span> <span data-ttu-id="78c41-159">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="78c41-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="78c41-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="78c41-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
1. <span data-ttu-id="78c41-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="78c41-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_certificate.png) 

1. <span data-ttu-id="78c41-163">BenSelect application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="78c41-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="78c41-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="78c41-164">Configure the following claims for this application.</span></span> <span data-ttu-id="78c41-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="78c41-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="78c41-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="78c41-166">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_06.png)

1. <span data-ttu-id="78c41-168">In the **User Attributes** section on the **Single sign-on** dialog:</span><span class="sxs-lookup"><span data-stu-id="78c41-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="78c41-169">a.</span><span class="sxs-lookup"><span data-stu-id="78c41-169">a.</span></span> <span data-ttu-id="78c41-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="78c41-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="78c41-171">b.</span><span class="sxs-lookup"><span data-stu-id="78c41-171">b.</span></span> <span data-ttu-id="78c41-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="78c41-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

1. <span data-ttu-id="78c41-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="78c41-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="78c41-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="78c41-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78c41-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="78c41-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_configure.png) 

1. <span data-ttu-id="78c41-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="78c41-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="78c41-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span><span class="sxs-lookup"><span data-stu-id="78c41-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="78c41-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="78c41-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78c41-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="78c41-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78c41-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78c41-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78c41-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="78c41-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="78c41-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78c41-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="78c41-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="78c41-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78c41-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="78c41-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/benselect-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="78c41-189">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="78c41-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/benselect-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="78c41-191">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="78c41-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/benselect-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="78c41-193">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="78c41-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78c41-195">a.</span><span class="sxs-lookup"><span data-stu-id="78c41-195">a.</span></span> <span data-ttu-id="78c41-196">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78c41-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78c41-197">b.</span><span class="sxs-lookup"><span data-stu-id="78c41-197">b.</span></span> <span data-ttu-id="78c41-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78c41-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78c41-199">c.</span><span class="sxs-lookup"><span data-stu-id="78c41-199">c.</span></span> <span data-ttu-id="78c41-200">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="78c41-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78c41-201">d.</span><span class="sxs-lookup"><span data-stu-id="78c41-201">d.</span></span> <span data-ttu-id="78c41-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="78c41-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="78c41-203">Creating a BenSelect test user</span><span class="sxs-lookup"><span data-stu-id="78c41-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="78c41-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span><span class="sxs-lookup"><span data-stu-id="78c41-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="78c41-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span><span class="sxs-lookup"><span data-stu-id="78c41-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78c41-206">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="78c41-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78c41-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span><span class="sxs-lookup"><span data-stu-id="78c41-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Assign User][200] 

<span data-ttu-id="78c41-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="78c41-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="78c41-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="78c41-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="78c41-212">In the applications list, select **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="78c41-212">In the applications list, select **BenSelect**.</span></span>

    ![Configure Single Sign-On](./media/benselect-tutorial/tutorial_benselect_app.png) 

1. <span data-ttu-id="78c41-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="78c41-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="78c41-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="78c41-216">Click **Add** button.</span></span> <span data-ttu-id="78c41-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="78c41-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="78c41-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="78c41-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="78c41-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="78c41-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="78c41-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="78c41-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78c41-222">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="78c41-222">Testing single sign-on</span></span>

<span data-ttu-id="78c41-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="78c41-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="78c41-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span><span class="sxs-lookup"><span data-stu-id="78c41-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78c41-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="78c41-225">Additional resources</span></span>

* [<span data-ttu-id="78c41-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78c41-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="78c41-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78c41-227">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/benselect-tutorial/tutorial_general_01.png
[2]: ./media/benselect-tutorial/tutorial_general_02.png
[3]: ./media/benselect-tutorial/tutorial_general_03.png
[4]: ./media/benselect-tutorial/tutorial_general_04.png

[100]: ./media/benselect-tutorial/tutorial_general_100.png

[200]: ./media/benselect-tutorial/tutorial_general_200.png
[201]: ./media/benselect-tutorial/tutorial_general_201.png
[202]: ./media/benselect-tutorial/tutorial_general_202.png
[203]: ./media/benselect-tutorial/tutorial_general_203.png

