---
title: 'Tutorial: Azure Active Directory integration with BetterWorks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 11e496b91eabeb6034cba25c8d0c1f87855467f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865969"
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="cb915-103">Tutorial: Azure Active Directory integration with BetterWorks</span><span class="sxs-lookup"><span data-stu-id="cb915-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="cb915-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb915-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb915-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cb915-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb915-106">You can control in Azure AD who has access to BetterWorks</span><span class="sxs-lookup"><span data-stu-id="cb915-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="cb915-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cb915-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb915-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cb915-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb915-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cb915-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb915-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cb915-110">Prerequisites</span></span>

<span data-ttu-id="cb915-111">To configure Azure AD integration with BetterWorks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cb915-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="cb915-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cb915-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb915-113">A BetterWorks single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cb915-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb915-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cb915-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb915-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cb915-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb915-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cb915-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb915-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb915-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb915-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cb915-118">Scenario description</span></span>
<span data-ttu-id="cb915-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cb915-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb915-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cb915-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb915-121">Adding BetterWorks from the gallery</span><span class="sxs-lookup"><span data-stu-id="cb915-121">Adding BetterWorks from the gallery</span></span>
1. <span data-ttu-id="cb915-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cb915-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="cb915-123">Adding BetterWorks from the gallery</span><span class="sxs-lookup"><span data-stu-id="cb915-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="cb915-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cb915-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb915-125">**To add BetterWorks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb915-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb915-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cb915-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cb915-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cb915-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb915-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cb915-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cb915-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cb915-133">In the search box, type **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="cb915-133">In the search box, type **BetterWorks**.</span></span>

    ![Creating an Azure AD test user](./media/betterworks-tutorial/tutorial_betterworks_search.png)

1. <span data-ttu-id="cb915-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cb915-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb915-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cb915-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb915-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="cb915-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb915-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb915-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="cb915-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cb915-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="cb915-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cb915-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb915-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cb915-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb915-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cb915-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cb915-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb915-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cb915-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cb915-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cb915-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cb915-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cb915-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cb915-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb915-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cb915-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb915-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span><span class="sxs-lookup"><span data-stu-id="cb915-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="cb915-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb915-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="cb915-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cb915-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cb915-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cb915-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_samlbase.png)

1. <span data-ttu-id="cb915-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span><span class="sxs-lookup"><span data-stu-id="cb915-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="cb915-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb915-157">a.</span></span> <span data-ttu-id="cb915-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="cb915-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="cb915-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb915-159">b.</span></span> <span data-ttu-id="cb915-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="cb915-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

1. <span data-ttu-id="cb915-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cb915-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="cb915-163">a.</span><span class="sxs-lookup"><span data-stu-id="cb915-163">a.</span></span> <span data-ttu-id="cb915-164">Click on the **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="cb915-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="cb915-165">b.</span><span class="sxs-lookup"><span data-stu-id="cb915-165">b.</span></span> <span data-ttu-id="cb915-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="cb915-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb915-167">These are not real values.</span><span class="sxs-lookup"><span data-stu-id="cb915-167">These are not real values.</span></span> <span data-ttu-id="cb915-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="cb915-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="cb915-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="cb915-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
1. <span data-ttu-id="cb915-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cb915-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_certificate.png)  

1. <span data-ttu-id="cb915-172">BetterWorks application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="cb915-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cb915-173">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="cb915-173">Configure the following claims for this application.</span></span> <span data-ttu-id="cb915-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span><span class="sxs-lookup"><span data-stu-id="cb915-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="cb915-175">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="cb915-175">The following screenshot shows an example for this.</span></span> 

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_attribute.png)

1. <span data-ttu-id="cb915-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cb915-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="cb915-178">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="cb915-178">Attribute Name</span></span> | <span data-ttu-id="cb915-179">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="cb915-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="cb915-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="cb915-180">saml_token</span></span>     | <span data-ttu-id="cb915-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="cb915-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="cb915-182">a.</span><span class="sxs-lookup"><span data-stu-id="cb915-182">a.</span></span> <span data-ttu-id="cb915-183">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="cb915-186">b.</span><span class="sxs-lookup"><span data-stu-id="cb915-186">b.</span></span> <span data-ttu-id="cb915-187">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="cb915-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="cb915-188">c.</span><span class="sxs-lookup"><span data-stu-id="cb915-188">c.</span></span> <span data-ttu-id="cb915-189">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="cb915-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="cb915-190">d.</span><span class="sxs-lookup"><span data-stu-id="cb915-190">d.</span></span> <span data-ttu-id="cb915-191">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="cb915-191">Click **Ok**.</span></span>

1. <span data-ttu-id="cb915-192">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cb915-192">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cb915-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="cb915-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="cb915-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cb915-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb915-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cb915-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb915-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb915-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb915-198">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cb915-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb915-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb915-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cb915-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb915-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb915-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cb915-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/betterworks-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cb915-204">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cb915-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/betterworks-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cb915-206">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/betterworks-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cb915-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cb915-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb915-210">a.</span><span class="sxs-lookup"><span data-stu-id="cb915-210">a.</span></span> <span data-ttu-id="cb915-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb915-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb915-212">b.</span><span class="sxs-lookup"><span data-stu-id="cb915-212">b.</span></span> <span data-ttu-id="cb915-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb915-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb915-214">c.</span><span class="sxs-lookup"><span data-stu-id="cb915-214">c.</span></span> <span data-ttu-id="cb915-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cb915-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb915-216">d.</span><span class="sxs-lookup"><span data-stu-id="cb915-216">d.</span></span> <span data-ttu-id="cb915-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb915-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="cb915-218">Creating a BetterWorks test user</span><span class="sxs-lookup"><span data-stu-id="cb915-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="cb915-219">In this section, you create a user called Britta Simon in BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="cb915-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="cb915-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span><span class="sxs-lookup"><span data-stu-id="cb915-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb915-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cb915-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb915-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="cb915-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Assign User][200] 

<span data-ttu-id="cb915-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cb915-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="cb915-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cb915-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cb915-227">In the applications list, select **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="cb915-227">In the applications list, select **BetterWorks**.</span></span>

    ![Configure Single Sign-On](./media/betterworks-tutorial/tutorial_betterworks_app.png) 

1. <span data-ttu-id="cb915-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cb915-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cb915-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cb915-231">Click **Add** button.</span></span> <span data-ttu-id="cb915-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cb915-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cb915-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cb915-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cb915-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cb915-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb915-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cb915-237">Testing single sign-on</span></span>

<span data-ttu-id="cb915-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cb915-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cb915-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span><span class="sxs-lookup"><span data-stu-id="cb915-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb915-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cb915-240">Additional resources</span></span>

* [<span data-ttu-id="cb915-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb915-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cb915-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb915-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/betterworks-tutorial/tutorial_general_01.png
[2]: ./media/betterworks-tutorial/tutorial_general_02.png
[3]: ./media/betterworks-tutorial/tutorial_general_03.png
[4]: ./media/betterworks-tutorial/tutorial_general_04.png

[100]: ./media/betterworks-tutorial/tutorial_general_100.png

[200]: ./media/betterworks-tutorial/tutorial_general_200.png
[201]: ./media/betterworks-tutorial/tutorial_general_201.png
[202]: ./media/betterworks-tutorial/tutorial_general_202.png
[203]: ./media/betterworks-tutorial/tutorial_general_203.png

