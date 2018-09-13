---
title: 'Tutorial: Azure Active Directory integration with UltiPro | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and UltiPro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 6a04bfe70f31175f046b1a16b3c00e22754200f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869660"
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="363ab-103">Tutorial: Azure Active Directory integration with UltiPro</span><span class="sxs-lookup"><span data-stu-id="363ab-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="363ab-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="363ab-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="363ab-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="363ab-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="363ab-106">You can control in Azure AD who has access to UltiPro</span><span class="sxs-lookup"><span data-stu-id="363ab-106">You can control in Azure AD who has access to UltiPro</span></span>
- <span data-ttu-id="363ab-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="363ab-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="363ab-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="363ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="363ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="363ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="363ab-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="363ab-110">Prerequisites</span></span>

<span data-ttu-id="363ab-111">To configure Azure AD integration with UltiPro, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="363ab-111">To configure Azure AD integration with UltiPro, you need the following items:</span></span>

- <span data-ttu-id="363ab-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="363ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="363ab-113">A UltiPro single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="363ab-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="363ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="363ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="363ab-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="363ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="363ab-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="363ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="363ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="363ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="363ab-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="363ab-118">Scenario description</span></span>
<span data-ttu-id="363ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="363ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="363ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="363ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="363ab-121">Adding UltiPro from the gallery</span><span class="sxs-lookup"><span data-stu-id="363ab-121">Adding UltiPro from the gallery</span></span>
1. <span data-ttu-id="363ab-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="363ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-the-gallery"></a><span data-ttu-id="363ab-123">Adding UltiPro from the gallery</span><span class="sxs-lookup"><span data-stu-id="363ab-123">Adding UltiPro from the gallery</span></span>
<span data-ttu-id="363ab-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="363ab-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="363ab-125">**To add UltiPro from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="363ab-125">**To add UltiPro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="363ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="363ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="363ab-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="363ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="363ab-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="363ab-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="363ab-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="363ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="363ab-133">In the search box, type **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="363ab-133">In the search box, type **UltiPro**.</span></span>

    ![Creating an Azure AD test user](./media/ultipro-tutorial/tutorial_ultipro_search.png)

1. <span data-ttu-id="363ab-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="363ab-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="363ab-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="363ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="363ab-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="363ab-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="363ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="363ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span></span> <span data-ttu-id="363ab-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span><span class="sxs-lookup"><span data-stu-id="363ab-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span></span>

<span data-ttu-id="363ab-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="363ab-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="363ab-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="363ab-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="363ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="363ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="363ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="363ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="363ab-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="363ab-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="363ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="363ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="363ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="363ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="363ab-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="363ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="363ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span><span class="sxs-lookup"><span data-stu-id="363ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="363ab-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="363ab-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="363ab-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="363ab-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="363ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="363ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_ultipro_samlbase.png)

1. <span data-ttu-id="363ab-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="363ab-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="363ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="363ab-157">a.</span></span> <span data-ttu-id="363ab-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="363ab-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="363ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="363ab-159">b.</span></span> <span data-ttu-id="363ab-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="363ab-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="363ab-161">c.</span><span class="sxs-lookup"><span data-stu-id="363ab-161">c.</span></span> <span data-ttu-id="363ab-162">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="363ab-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="363ab-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="363ab-163">These values are not real.</span></span> <span data-ttu-id="363ab-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="363ab-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="363ab-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span><span class="sxs-lookup"><span data-stu-id="363ab-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span></span> 

1. <span data-ttu-id="363ab-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="363ab-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_ultipro_certificate.png) 

1. <span data-ttu-id="363ab-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="363ab-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="363ab-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="363ab-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span></span> <span data-ttu-id="363ab-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="363ab-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_ultipro_configure.png) 

1. <span data-ttu-id="363ab-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="363ab-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="363ab-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="363ab-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="363ab-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="363ab-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="363ab-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="363ab-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="363ab-177">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="363ab-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="363ab-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="363ab-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="363ab-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="363ab-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="363ab-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="363ab-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/ultipro-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="363ab-183">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="363ab-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/ultipro-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="363ab-185">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="363ab-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/ultipro-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="363ab-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="363ab-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="363ab-189">a.</span><span class="sxs-lookup"><span data-stu-id="363ab-189">a.</span></span> <span data-ttu-id="363ab-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="363ab-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="363ab-191">b.</span><span class="sxs-lookup"><span data-stu-id="363ab-191">b.</span></span> <span data-ttu-id="363ab-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="363ab-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="363ab-193">c.</span><span class="sxs-lookup"><span data-stu-id="363ab-193">c.</span></span> <span data-ttu-id="363ab-194">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="363ab-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="363ab-195">d.</span><span class="sxs-lookup"><span data-stu-id="363ab-195">d.</span></span> <span data-ttu-id="363ab-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="363ab-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="363ab-197">Creating a UltiPro test user</span><span class="sxs-lookup"><span data-stu-id="363ab-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="363ab-198">In this section, you create a user called Britta Simon in UltiPro.</span><span class="sxs-lookup"><span data-stu-id="363ab-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="363ab-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span><span class="sxs-lookup"><span data-stu-id="363ab-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span></span> <span data-ttu-id="363ab-200">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="363ab-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="363ab-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="363ab-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="363ab-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span><span class="sxs-lookup"><span data-stu-id="363ab-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span></span>

![Assign User][200] 

<span data-ttu-id="363ab-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="363ab-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="363ab-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="363ab-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="363ab-207">In the applications list, select **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="363ab-207">In the applications list, select **UltiPro**.</span></span>

    ![Configure Single Sign-On](./media/ultipro-tutorial/tutorial_ultipro_app.png) 

1. <span data-ttu-id="363ab-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="363ab-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="363ab-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="363ab-211">Click **Add** button.</span></span> <span data-ttu-id="363ab-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="363ab-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="363ab-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="363ab-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="363ab-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="363ab-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="363ab-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="363ab-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="363ab-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="363ab-217">Testing single sign-on</span></span>

<span data-ttu-id="363ab-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="363ab-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="363ab-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span><span class="sxs-lookup"><span data-stu-id="363ab-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="363ab-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="363ab-220">Additional resources</span></span>

* [<span data-ttu-id="363ab-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="363ab-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="363ab-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="363ab-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ultipro-tutorial/tutorial_general_01.png
[2]: ./media/ultipro-tutorial/tutorial_general_02.png
[3]: ./media/ultipro-tutorial/tutorial_general_03.png
[4]: ./media/ultipro-tutorial/tutorial_general_04.png

[100]: ./media/ultipro-tutorial/tutorial_general_100.png

[200]: ./media/ultipro-tutorial/tutorial_general_200.png
[201]: ./media/ultipro-tutorial/tutorial_general_201.png
[202]: ./media/ultipro-tutorial/tutorial_general_202.png
[203]: ./media/ultipro-tutorial/tutorial_general_203.png

