---
title: 'Tutorial: Azure Active Directory integration with Collaborative Innovation | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Collaborative Innovation.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 14dc0befdfe92970c194de852f6ef2dc98080ae7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871183"
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="917d5-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="917d5-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="917d5-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="917d5-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="917d5-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="917d5-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="917d5-106">You can control in Azure AD who has access to Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="917d5-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="917d5-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="917d5-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="917d5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="917d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="917d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="917d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="917d5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="917d5-110">Prerequisites</span></span>

<span data-ttu-id="917d5-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="917d5-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="917d5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="917d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="917d5-113">A Collaborative Innovation single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="917d5-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="917d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="917d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="917d5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="917d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="917d5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="917d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="917d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="917d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="917d5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="917d5-118">Scenario description</span></span>
<span data-ttu-id="917d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="917d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="917d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="917d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="917d5-121">Adding Collaborative Innovation from the gallery</span><span class="sxs-lookup"><span data-stu-id="917d5-121">Adding Collaborative Innovation from the gallery</span></span>
1. <span data-ttu-id="917d5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="917d5-123">Adding Collaborative Innovation from the gallery</span><span class="sxs-lookup"><span data-stu-id="917d5-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="917d5-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="917d5-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="917d5-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917d5-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="917d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="917d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="917d5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="917d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="917d5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="917d5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="917d5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="917d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="917d5-133">In the search box, type **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="917d5-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

1. <span data-ttu-id="917d5-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="917d5-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="917d5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="917d5-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="917d5-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="917d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="917d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="917d5-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span><span class="sxs-lookup"><span data-stu-id="917d5-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="917d5-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="917d5-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="917d5-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="917d5-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="917d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="917d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="917d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="917d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="917d5-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="917d5-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="917d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="917d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="917d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="917d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="917d5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="917d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span><span class="sxs-lookup"><span data-stu-id="917d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="917d5-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917d5-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="917d5-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="917d5-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="917d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="917d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

1. <span data-ttu-id="917d5-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="917d5-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="917d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="917d5-157">a.</span></span> <span data-ttu-id="917d5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="917d5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="917d5-159">b.</span><span class="sxs-lookup"><span data-stu-id="917d5-159">b.</span></span> <span data-ttu-id="917d5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="917d5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="917d5-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="917d5-161">These values are not real.</span></span> <span data-ttu-id="917d5-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="917d5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="917d5-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="917d5-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

1. <span data-ttu-id="917d5-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="917d5-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="917d5-165">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="917d5-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="917d5-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="917d5-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="917d5-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="917d5-167">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/attribute.png)
    
1. <span data-ttu-id="917d5-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="917d5-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="917d5-170">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="917d5-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="917d5-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="917d5-171">Attribute Name</span></span> | <span data-ttu-id="917d5-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="917d5-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="917d5-173">givenname</span><span class="sxs-lookup"><span data-stu-id="917d5-173">givenname</span></span> | <span data-ttu-id="917d5-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="917d5-174">user.givenname</span></span> |
    | <span data-ttu-id="917d5-175">surname</span><span class="sxs-lookup"><span data-stu-id="917d5-175">surname</span></span> | <span data-ttu-id="917d5-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="917d5-176">user.surname</span></span> |
    | <span data-ttu-id="917d5-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="917d5-177">emailaddress</span></span> | <span data-ttu-id="917d5-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="917d5-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="917d5-179">name</span><span class="sxs-lookup"><span data-stu-id="917d5-179">name</span></span> | <span data-ttu-id="917d5-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="917d5-180">user.userprincipalname</span></span> |

    <span data-ttu-id="917d5-181">a.</span><span class="sxs-lookup"><span data-stu-id="917d5-181">a.</span></span> <span data-ttu-id="917d5-182">Click the attribute to open the **Edit Attribute** window.</span><span class="sxs-lookup"><span data-stu-id="917d5-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="917d5-184">b.</span><span class="sxs-lookup"><span data-stu-id="917d5-184">b.</span></span> <span data-ttu-id="917d5-185">Delete the URL value from the **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="917d5-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="917d5-186">c.</span><span class="sxs-lookup"><span data-stu-id="917d5-186">c.</span></span> <span data-ttu-id="917d5-187">Click **Ok** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="917d5-187">Click **Ok** to save the setting.</span></span>

1. <span data-ttu-id="917d5-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="917d5-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

1. <span data-ttu-id="917d5-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="917d5-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="917d5-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="917d5-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="917d5-193">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="917d5-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="917d5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="917d5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="917d5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="917d5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="917d5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="917d5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="917d5-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="917d5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="917d5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="917d5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="917d5-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917d5-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="917d5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="917d5-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="917d5-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="917d5-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="917d5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="917d5-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="917d5-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="917d5-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="917d5-209">a.</span><span class="sxs-lookup"><span data-stu-id="917d5-209">a.</span></span> <span data-ttu-id="917d5-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="917d5-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="917d5-211">b.</span><span class="sxs-lookup"><span data-stu-id="917d5-211">b.</span></span> <span data-ttu-id="917d5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="917d5-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="917d5-213">c.</span><span class="sxs-lookup"><span data-stu-id="917d5-213">c.</span></span> <span data-ttu-id="917d5-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="917d5-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="917d5-215">d.</span><span class="sxs-lookup"><span data-stu-id="917d5-215">d.</span></span> <span data-ttu-id="917d5-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="917d5-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="917d5-217">Creating a Collaborative Innovation test user</span><span class="sxs-lookup"><span data-stu-id="917d5-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="917d5-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="917d5-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="917d5-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="917d5-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="917d5-220">So there is no need to perform any steps here.</span><span class="sxs-lookup"><span data-stu-id="917d5-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="917d5-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="917d5-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="917d5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="917d5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Assign User][200] 

<span data-ttu-id="917d5-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917d5-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="917d5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="917d5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="917d5-227">In the applications list, select **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="917d5-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Configure Single Sign-On](./media/collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

1. <span data-ttu-id="917d5-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="917d5-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="917d5-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="917d5-231">Click **Add** button.</span></span> <span data-ttu-id="917d5-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="917d5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="917d5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="917d5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="917d5-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="917d5-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="917d5-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="917d5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="917d5-237">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="917d5-237">Testing single sign-on</span></span>

<span data-ttu-id="917d5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="917d5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="917d5-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span><span class="sxs-lookup"><span data-stu-id="917d5-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="917d5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="917d5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="917d5-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="917d5-241">Additional resources</span></span>

* [<span data-ttu-id="917d5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="917d5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="917d5-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="917d5-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/collaborativeinnovation-tutorial/tutorial_general_203.png

