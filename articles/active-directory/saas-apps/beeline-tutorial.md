---
title: 'Tutorial: Azure Active Directory integration with BeeLine | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BeeLine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6ae549d7a58c35438345e43a178a3ea12630efe7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856954"
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="4396a-103">Tutorial: Azure Active Directory integration with BeeLine</span><span class="sxs-lookup"><span data-stu-id="4396a-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="4396a-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4396a-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4396a-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4396a-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4396a-106">You can control in Azure AD who has access to BeeLine</span><span class="sxs-lookup"><span data-stu-id="4396a-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="4396a-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4396a-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4396a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4396a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4396a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4396a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4396a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4396a-110">Prerequisites</span></span>

<span data-ttu-id="4396a-111">To configure Azure AD integration with BeeLine, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4396a-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="4396a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4396a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4396a-113">A BeeLine single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4396a-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4396a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4396a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4396a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4396a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4396a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4396a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4396a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4396a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4396a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4396a-118">Scenario description</span></span>
<span data-ttu-id="4396a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4396a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4396a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4396a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4396a-121">Adding BeeLine from the gallery</span><span class="sxs-lookup"><span data-stu-id="4396a-121">Adding BeeLine from the gallery</span></span>
1. <span data-ttu-id="4396a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4396a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="4396a-123">Adding BeeLine from the gallery</span><span class="sxs-lookup"><span data-stu-id="4396a-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="4396a-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4396a-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4396a-125">**To add BeeLine from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4396a-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4396a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4396a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4396a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4396a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4396a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4396a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4396a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4396a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4396a-133">In the search box, type **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="4396a-133">In the search box, type **BeeLine**.</span></span>

    ![Creating an Azure AD test user](./media/beeline-tutorial/tutorial_beeline_search.png)

1. <span data-ttu-id="4396a-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4396a-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4396a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4396a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4396a-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4396a-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4396a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4396a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="4396a-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4396a-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="4396a-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4396a-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4396a-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4396a-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4396a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4396a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4396a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4396a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4396a-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4396a-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4396a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4396a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4396a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4396a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4396a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4396a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4396a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span><span class="sxs-lookup"><span data-stu-id="4396a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="4396a-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4396a-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="4396a-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4396a-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4396a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4396a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_beeline_samlbase.png)

1. <span data-ttu-id="4396a-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4396a-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="4396a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4396a-157">a.</span></span> <span data-ttu-id="4396a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="4396a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="4396a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4396a-159">b.</span></span> <span data-ttu-id="4396a-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="4396a-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="4396a-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4396a-161">These values are not real.</span></span> <span data-ttu-id="4396a-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="4396a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4396a-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4396a-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
1. <span data-ttu-id="4396a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4396a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_beeline_certificate.png) 

1. <span data-ttu-id="4396a-166">Your Beeline application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="4396a-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="4396a-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span><span class="sxs-lookup"><span data-stu-id="4396a-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="4396a-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span><span class="sxs-lookup"><span data-stu-id="4396a-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="4396a-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="4396a-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="4396a-170">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="4396a-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="4396a-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span><span class="sxs-lookup"><span data-stu-id="4396a-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_attribute.png)    

1. <span data-ttu-id="4396a-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4396a-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4396a-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4396a-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4396a-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4396a-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_beeline_configure.png) 

1. <span data-ttu-id="4396a-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="4396a-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="4396a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4396a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4396a-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4396a-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4396a-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4396a-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4396a-182">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4396a-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="4396a-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4396a-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4396a-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4396a-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4396a-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4396a-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/beeline-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4396a-188">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4396a-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/beeline-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4396a-190">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4396a-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/beeline-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4396a-192">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4396a-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4396a-194">a.</span><span class="sxs-lookup"><span data-stu-id="4396a-194">a.</span></span> <span data-ttu-id="4396a-195">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4396a-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4396a-196">b.</span><span class="sxs-lookup"><span data-stu-id="4396a-196">b.</span></span> <span data-ttu-id="4396a-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4396a-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4396a-198">c.</span><span class="sxs-lookup"><span data-stu-id="4396a-198">c.</span></span> <span data-ttu-id="4396a-199">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4396a-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4396a-200">d.</span><span class="sxs-lookup"><span data-stu-id="4396a-200">d.</span></span> <span data-ttu-id="4396a-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4396a-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="4396a-202">Creating a BeeLine test user</span><span class="sxs-lookup"><span data-stu-id="4396a-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="4396a-203">In this section, you create a user called Britta Simon in Beeline.</span><span class="sxs-lookup"><span data-stu-id="4396a-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="4396a-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="4396a-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="4396a-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span><span class="sxs-lookup"><span data-stu-id="4396a-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4396a-206">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4396a-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4396a-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span><span class="sxs-lookup"><span data-stu-id="4396a-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Assign User][200] 

<span data-ttu-id="4396a-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4396a-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="4396a-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4396a-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4396a-212">In the applications list, select **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="4396a-212">In the applications list, select **BeeLine**.</span></span>

    ![Configure Single Sign-On](./media/beeline-tutorial/tutorial_beeline_app.png) 

1. <span data-ttu-id="4396a-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4396a-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4396a-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4396a-216">Click **Add** button.</span></span> <span data-ttu-id="4396a-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4396a-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4396a-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4396a-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4396a-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4396a-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4396a-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4396a-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4396a-222">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4396a-222">Testing single sign-on</span></span>

<span data-ttu-id="4396a-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4396a-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="4396a-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span><span class="sxs-lookup"><span data-stu-id="4396a-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4396a-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4396a-225">Additional resources</span></span>

* [<span data-ttu-id="4396a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4396a-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4396a-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4396a-227">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/beeline-tutorial/tutorial_general_01.png
[2]: ./media/beeline-tutorial/tutorial_general_02.png
[3]: ./media/beeline-tutorial/tutorial_general_03.png
[4]: ./media/beeline-tutorial/tutorial_general_04.png

[100]: ./media/beeline-tutorial/tutorial_general_100.png

[200]: ./media/beeline-tutorial/tutorial_general_200.png
[201]: ./media/beeline-tutorial/tutorial_general_201.png
[202]: ./media/beeline-tutorial/tutorial_general_202.png
[203]: ./media/beeline-tutorial/tutorial_general_203.png

