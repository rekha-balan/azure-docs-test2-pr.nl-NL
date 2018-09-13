---
title: 'Tutorial: Azure Active Directory integration with Neota Logic Studio | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Neota Logic Studio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 667d2a5217f5c2aa29432a99cd0e07fc8d7b3ca7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870185"
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="5c6e8-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="5c6e8-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="5c6e8-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c6e8-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c6e8-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c6e8-106">You can control in Azure AD who has access to Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="5c6e8-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="5c6e8-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5c6e8-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c6e8-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5c6e8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c6e8-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5c6e8-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5c6e8-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c6e8-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5c6e8-111">Prerequisites</span></span>

<span data-ttu-id="5c6e8-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="5c6e8-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5c6e8-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5c6e8-114">A Neota Logic Studio single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5c6e8-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c6e8-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c6e8-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c6e8-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c6e8-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c6e8-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c6e8-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5c6e8-119">Scenario description</span></span>

<span data-ttu-id="5c6e8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c6e8-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c6e8-122">Adding Neota Logic Studio from the gallery</span><span class="sxs-lookup"><span data-stu-id="5c6e8-122">Adding Neota Logic Studio from the gallery</span></span>
1. <span data-ttu-id="5c6e8-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c6e8-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="5c6e8-124">Adding Neota Logic Studio from the gallery</span><span class="sxs-lookup"><span data-stu-id="5c6e8-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="5c6e8-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c6e8-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c6e8-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c6e8-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="5c6e8-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c6e8-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="5c6e8-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="5c6e8-134">In the search box, type **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

1. <span data-ttu-id="5c6e8-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c6e8-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c6e8-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5c6e8-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5c6e8-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c6e8-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="5c6e8-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="5c6e8-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="5c6e8-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c6e8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="5c6e8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="5c6e8-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="5c6e8-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="5c6e8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c6e8-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c6e8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c6e8-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="5c6e8-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c6e8-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="5c6e8-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="5c6e8-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

1. <span data-ttu-id="5c6e8-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="5c6e8-158">a.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-158">a.</span></span> <span data-ttu-id="5c6e8-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="5c6e8-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="5c6e8-160">b.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-160">b.</span></span> <span data-ttu-id="5c6e8-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="5c6e8-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c6e8-162">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-162">These values are not the real.</span></span> <span data-ttu-id="5c6e8-163">Update these values with the actual Sign-On URL & Identifier.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="5c6e8-164">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="5c6e8-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
1. <span data-ttu-id="5c6e8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

1. <span data-ttu-id="5c6e8-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/neotalogicstudio-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="5c6e8-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="5c6e8-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="5c6e8-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c6e8-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c6e8-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c6e8-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c6e8-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5c6e8-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c6e8-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="5c6e8-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c6e8-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c6e8-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="5c6e8-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="5c6e8-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="5c6e8-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5c6e8-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c6e8-186">a.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-186">a.</span></span> <span data-ttu-id="5c6e8-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c6e8-188">b.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-188">b.</span></span> <span data-ttu-id="5c6e8-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c6e8-190">c.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-190">c.</span></span> <span data-ttu-id="5c6e8-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c6e8-192">d.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-192">d.</span></span> <span data-ttu-id="5c6e8-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="5c6e8-194">Creating a Neota Logic Studio test user</span><span class="sxs-lookup"><span data-stu-id="5c6e8-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="5c6e8-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="5c6e8-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="5c6e8-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c6e8-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5c6e8-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c6e8-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Assign User][200] 

<span data-ttu-id="5c6e8-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5c6e8-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="5c6e8-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="5c6e8-204">In the applications list, select **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Configure Single Sign-On](./media/neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

1. <span data-ttu-id="5c6e8-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="5c6e8-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-208">Click **Add** button.</span></span> <span data-ttu-id="5c6e8-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="5c6e8-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="5c6e8-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="5c6e8-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c6e8-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="5c6e8-214">Testing single sign-on</span></span>

<span data-ttu-id="5c6e8-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c6e8-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="5c6e8-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span><span class="sxs-lookup"><span data-stu-id="5c6e8-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="5c6e8-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c6e8-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c6e8-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5c6e8-219">Additional resources</span></span>

* [<span data-ttu-id="5c6e8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c6e8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5c6e8-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c6e8-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/neotalogicstudio-tutorial/tutorial_general_203.png

