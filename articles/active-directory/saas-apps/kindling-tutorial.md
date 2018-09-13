---
title: 'Tutorial: Azure Active Directory integration with Kindling | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kindling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: af92553b0b88febf86eb9aebaad99c7c3ddff792
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856933"
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="a182c-103">Tutorial: Azure Active Directory integration with Kindling</span><span class="sxs-lookup"><span data-stu-id="a182c-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="a182c-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a182c-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a182c-105">Integrating Kindling with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a182c-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a182c-106">You can control in Azure AD who has access to Kindling</span><span class="sxs-lookup"><span data-stu-id="a182c-106">You can control in Azure AD who has access to Kindling</span></span>
- <span data-ttu-id="a182c-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a182c-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a182c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a182c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a182c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="a182c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a182c-110">[what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a182c-110">[what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a182c-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a182c-111">Prerequisites</span></span>

<span data-ttu-id="a182c-112">To configure Azure AD integration with Kindling, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a182c-112">To configure Azure AD integration with Kindling, you need the following items:</span></span>

- <span data-ttu-id="a182c-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a182c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a182c-114">A Kindling single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a182c-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a182c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a182c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a182c-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a182c-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a182c-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a182c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a182c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a182c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a182c-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a182c-119">Scenario description</span></span>
<span data-ttu-id="a182c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a182c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a182c-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a182c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a182c-122">Adding Kindling from the gallery</span><span class="sxs-lookup"><span data-stu-id="a182c-122">Adding Kindling from the gallery</span></span>
1. <span data-ttu-id="a182c-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a182c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="a182c-124">Adding Kindling from the gallery</span><span class="sxs-lookup"><span data-stu-id="a182c-124">Adding Kindling from the gallery</span></span>
<span data-ttu-id="a182c-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a182c-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a182c-126">**To add Kindling from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a182c-126">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a182c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a182c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a182c-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a182c-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a182c-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a182c-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a182c-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a182c-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a182c-134">In the search box, type **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="a182c-134">In the search box, type **Kindling**.</span></span>

    ![Creating an Azure AD test user](./media/kindling-tutorial/tutorial_kindling_search.png)

1. <span data-ttu-id="a182c-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a182c-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a182c-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a182c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a182c-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a182c-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a182c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a182c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span></span> <span data-ttu-id="a182c-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a182c-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>

<span data-ttu-id="a182c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span><span class="sxs-lookup"><span data-stu-id="a182c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="a182c-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a182c-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a182c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a182c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a182c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a182c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a182c-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a182c-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a182c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a182c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a182c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a182c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a182c-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a182c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a182c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span><span class="sxs-lookup"><span data-stu-id="a182c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="a182c-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a182c-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="a182c-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a182c-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a182c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a182c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_kindling_samlbase.png)

1. <span data-ttu-id="a182c-156">On the **Kindling Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a182c-156">On the **Kindling Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="a182c-158">a.</span><span class="sxs-lookup"><span data-stu-id="a182c-158">a.</span></span> <span data-ttu-id="a182c-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="a182c-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="a182c-160">b.</span><span class="sxs-lookup"><span data-stu-id="a182c-160">b.</span></span>  <span data-ttu-id="a182c-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="a182c-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a182c-162">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="a182c-162">These values are not the real.</span></span> <span data-ttu-id="a182c-163">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a182c-163">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a182c-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a182c-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span></span>
 
1. <span data-ttu-id="a182c-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a182c-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_kindling_certificate.png) 

1. <span data-ttu-id="a182c-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a182c-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a182c-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a182c-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a182c-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a182c-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_kindling_configure.png) 

1. <span data-ttu-id="a182c-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="a182c-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="a182c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a182c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a182c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a182c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a182c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a182c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a182c-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a182c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a182c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a182c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a182c-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a182c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a182c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a182c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kindling-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a182c-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a182c-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kindling-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a182c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a182c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kindling-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a182c-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a182c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a182c-188">a.</span><span class="sxs-lookup"><span data-stu-id="a182c-188">a.</span></span> <span data-ttu-id="a182c-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a182c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a182c-190">b.</span><span class="sxs-lookup"><span data-stu-id="a182c-190">b.</span></span> <span data-ttu-id="a182c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a182c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a182c-192">c.</span><span class="sxs-lookup"><span data-stu-id="a182c-192">c.</span></span> <span data-ttu-id="a182c-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a182c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a182c-194">d.</span><span class="sxs-lookup"><span data-stu-id="a182c-194">d.</span></span> <span data-ttu-id="a182c-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a182c-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="a182c-196">Creating a Kindling test user</span><span class="sxs-lookup"><span data-stu-id="a182c-196">Creating a Kindling test user</span></span>

<span data-ttu-id="a182c-197">The objective of this section is to create a user called Britta Simon in Kindling.</span><span class="sxs-lookup"><span data-stu-id="a182c-197">The objective of this section is to create a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="a182c-198">Kindling supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="a182c-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="a182c-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a182c-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="a182c-200">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a182c-200">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a182c-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a182c-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a182c-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span><span class="sxs-lookup"><span data-stu-id="a182c-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span></span>

![Assign User][200] 

<span data-ttu-id="a182c-204">**To assign Britta Simon to Kindling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a182c-204">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="a182c-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a182c-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a182c-207">In the applications list, select **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="a182c-207">In the applications list, select **Kindling**.</span></span>

    ![Configure Single Sign-On](./media/kindling-tutorial/tutorial_kindling_app.png) 

1. <span data-ttu-id="a182c-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a182c-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a182c-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a182c-211">Click **Add** button.</span></span> <span data-ttu-id="a182c-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a182c-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a182c-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a182c-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a182c-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a182c-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a182c-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a182c-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a182c-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a182c-217">Testing single sign-on</span></span>

<span data-ttu-id="a182c-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a182c-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a182c-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span><span class="sxs-lookup"><span data-stu-id="a182c-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a182c-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a182c-220">Additional resources</span></span>

* [<span data-ttu-id="a182c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a182c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a182c-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a182c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kindling-tutorial/tutorial_general_01.png
[2]: ./media/kindling-tutorial/tutorial_general_02.png
[3]: ./media/kindling-tutorial/tutorial_general_03.png
[4]: ./media/kindling-tutorial/tutorial_general_04.png

[100]: ./media/kindling-tutorial/tutorial_general_100.png

[200]: ./media/kindling-tutorial/tutorial_general_200.png
[201]: ./media/kindling-tutorial/tutorial_general_201.png
[202]: ./media/kindling-tutorial/tutorial_general_202.png
[203]: ./media/kindling-tutorial/tutorial_general_203.png

