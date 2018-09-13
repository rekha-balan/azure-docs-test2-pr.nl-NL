---
title: 'Tutorial: Azure Active Directory integration with Halogen Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Halogen Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a7be918118d86da7e1134f5ce46e5f163ba62601
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857603"
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="8d43b-103">Tutorial: Azure Active Directory integration with Halogen Software</span><span class="sxs-lookup"><span data-stu-id="8d43b-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="8d43b-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d43b-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d43b-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8d43b-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d43b-106">You can control in Azure AD who has access to Halogen Software</span><span class="sxs-lookup"><span data-stu-id="8d43b-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="8d43b-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8d43b-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d43b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8d43b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d43b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8d43b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d43b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d43b-110">Prerequisites</span></span>

<span data-ttu-id="8d43b-111">To configure Azure AD integration with Halogen Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8d43b-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="8d43b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8d43b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d43b-113">A Halogen Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8d43b-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d43b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8d43b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d43b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8d43b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d43b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8d43b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d43b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d43b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d43b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8d43b-118">Scenario description</span></span>

<span data-ttu-id="8d43b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8d43b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d43b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d43b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d43b-121">Adding Halogen Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d43b-121">Adding Halogen Software from the gallery</span></span>
1. <span data-ttu-id="8d43b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d43b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="8d43b-123">Adding Halogen Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d43b-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="8d43b-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8d43b-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d43b-125">**To add Halogen Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d43b-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d43b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8d43b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8d43b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d43b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8d43b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8d43b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8d43b-133">In the search box, type **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-133">In the search box, type **Halogen Software**.</span></span>

    ![Creating an Azure AD test user](./media/halogen-software-tutorial/tutorial_halogensoftware_search.png)

1. <span data-ttu-id="8d43b-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8d43b-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d43b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d43b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d43b-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d43b-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d43b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d43b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="8d43b-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8d43b-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="8d43b-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8d43b-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d43b-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d43b-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d43b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8d43b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8d43b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d43b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8d43b-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8d43b-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8d43b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d43b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8d43b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8d43b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d43b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d43b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d43b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span><span class="sxs-lookup"><span data-stu-id="8d43b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="8d43b-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d43b-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8d43b-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8d43b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d43b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

1. <span data-ttu-id="8d43b-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d43b-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="8d43b-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d43b-157">a.</span></span> <span data-ttu-id="8d43b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8d43b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="8d43b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d43b-159">b.</span></span> <span data-ttu-id="8d43b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8d43b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d43b-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8d43b-161">These values are not real.</span></span> <span data-ttu-id="8d43b-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="8d43b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d43b-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8d43b-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


1. <span data-ttu-id="8d43b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8d43b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

1. <span data-ttu-id="8d43b-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8d43b-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/halogen-software-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8d43b-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8d43b-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

1. <span data-ttu-id="8d43b-169">Click the **Options** tab.</span><span class="sxs-lookup"><span data-stu-id="8d43b-169">Click the **Options** tab.</span></span> 
   
    ![What is Azure AD Connect][12]

1. <span data-ttu-id="8d43b-171">In the left navigation pane, click **SAML Configuration**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![What is Azure AD Connect][13]

1. <span data-ttu-id="8d43b-173">On the **SAML Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d43b-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![What is Azure AD Connect][14]

     <span data-ttu-id="8d43b-175">a.</span><span class="sxs-lookup"><span data-stu-id="8d43b-175">a.</span></span> <span data-ttu-id="8d43b-176">As **Unique Identifier**, select **NameID**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="8d43b-177">b.</span><span class="sxs-lookup"><span data-stu-id="8d43b-177">b.</span></span> <span data-ttu-id="8d43b-178">As **Unique Identifier Maps To**, select **Username**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="8d43b-179">c.</span><span class="sxs-lookup"><span data-stu-id="8d43b-179">c.</span></span> <span data-ttu-id="8d43b-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="8d43b-181">d.</span><span class="sxs-lookup"><span data-stu-id="8d43b-181">d.</span></span> <span data-ttu-id="8d43b-182">To test the configuration, click **Run Test**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="8d43b-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span><span class="sxs-lookup"><span data-stu-id="8d43b-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="8d43b-184">Then, close the opened browser window.</span><span class="sxs-lookup"><span data-stu-id="8d43b-184">Then, close the opened browser window.</span></span> <span data-ttu-id="8d43b-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span><span class="sxs-lookup"><span data-stu-id="8d43b-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="8d43b-186">e.</span><span class="sxs-lookup"><span data-stu-id="8d43b-186">e.</span></span> <span data-ttu-id="8d43b-187">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="8d43b-188">f.</span><span class="sxs-lookup"><span data-stu-id="8d43b-188">f.</span></span> <span data-ttu-id="8d43b-189">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="8d43b-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8d43b-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d43b-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8d43b-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d43b-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d43b-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d43b-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d43b-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="8d43b-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d43b-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8d43b-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d43b-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d43b-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8d43b-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/halogen-software-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8d43b-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/halogen-software-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8d43b-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8d43b-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/halogen-software-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8d43b-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d43b-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d43b-205">a.</span><span class="sxs-lookup"><span data-stu-id="8d43b-205">a.</span></span> <span data-ttu-id="8d43b-206">In the **Name** textbox, type name as **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="8d43b-207">b.</span><span class="sxs-lookup"><span data-stu-id="8d43b-207">b.</span></span> <span data-ttu-id="8d43b-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d43b-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d43b-209">c.</span><span class="sxs-lookup"><span data-stu-id="8d43b-209">c.</span></span> <span data-ttu-id="8d43b-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d43b-211">d.</span><span class="sxs-lookup"><span data-stu-id="8d43b-211">d.</span></span> <span data-ttu-id="8d43b-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="8d43b-213">Creating a Halogen Software test user</span><span class="sxs-lookup"><span data-stu-id="8d43b-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="8d43b-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="8d43b-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="8d43b-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d43b-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8d43b-216">Sign on to your **Halogen Software** application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8d43b-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

1. <span data-ttu-id="8d43b-217">Click the **User Center** tab, and then click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![What is Azure AD Connect][300]  

1. <span data-ttu-id="8d43b-219">On the **New User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d43b-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![What is Azure AD Connect][301]

    <span data-ttu-id="8d43b-221">a.</span><span class="sxs-lookup"><span data-stu-id="8d43b-221">a.</span></span> <span data-ttu-id="8d43b-222">In the **First Name** textbox, type first name of the user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="8d43b-223">b.</span><span class="sxs-lookup"><span data-stu-id="8d43b-223">b.</span></span> <span data-ttu-id="8d43b-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="8d43b-225">c.</span><span class="sxs-lookup"><span data-stu-id="8d43b-225">c.</span></span> <span data-ttu-id="8d43b-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d43b-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="8d43b-227">d.</span><span class="sxs-lookup"><span data-stu-id="8d43b-227">d.</span></span> <span data-ttu-id="8d43b-228">In the **Password** textbox, type a password for Britta.</span><span class="sxs-lookup"><span data-stu-id="8d43b-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="8d43b-229">e.</span><span class="sxs-lookup"><span data-stu-id="8d43b-229">e.</span></span> <span data-ttu-id="8d43b-230">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d43b-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d43b-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d43b-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="8d43b-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Assign User][200] 

<span data-ttu-id="8d43b-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d43b-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="8d43b-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8d43b-237">In the applications list, select **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-237">In the applications list, select **Halogen Software**.</span></span>

    ![Configure Single Sign-On](./media/halogen-software-tutorial/tutorial_halogensoftware_app.png) 

1. <span data-ttu-id="8d43b-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8d43b-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8d43b-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8d43b-241">Click **Add** button.</span></span> <span data-ttu-id="8d43b-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d43b-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8d43b-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8d43b-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8d43b-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d43b-245">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8d43b-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d43b-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d43b-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d43b-247">Testing single sign-on</span></span>

<span data-ttu-id="8d43b-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8d43b-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8d43b-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span><span class="sxs-lookup"><span data-stu-id="8d43b-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d43b-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8d43b-250">Additional resources</span></span>

* [<span data-ttu-id="8d43b-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d43b-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8d43b-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d43b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/halogen-software-tutorial/tutorial_halogen_301.png
