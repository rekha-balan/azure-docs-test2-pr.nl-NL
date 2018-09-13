---
title: 'Tutorial: Azure Active Directory integration with Directions on Microsoft | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Directions on Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 08027326761736fe03e27b7a45ec11c0d514dc22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969062"
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="2de98-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="2de98-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="2de98-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2de98-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2de98-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2de98-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2de98-106">You can control in Azure AD who has access to Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="2de98-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="2de98-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2de98-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2de98-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2de98-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2de98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2de98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2de98-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2de98-110">Prerequisites</span></span>

<span data-ttu-id="2de98-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2de98-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="2de98-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2de98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2de98-113">A Directions on Microsoft single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2de98-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2de98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2de98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2de98-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2de98-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2de98-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2de98-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2de98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2de98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2de98-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2de98-118">Scenario description</span></span>
<span data-ttu-id="2de98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2de98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2de98-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2de98-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2de98-121">Adding Directions on Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="2de98-121">Adding Directions on Microsoft from the gallery</span></span>
1. <span data-ttu-id="2de98-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2de98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="2de98-123">Adding Directions on Microsoft from the gallery</span><span class="sxs-lookup"><span data-stu-id="2de98-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="2de98-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2de98-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2de98-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2de98-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2de98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2de98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="2de98-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2de98-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2de98-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2de98-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="2de98-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2de98-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="2de98-133">In the search box, type **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2de98-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

1. <span data-ttu-id="2de98-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2de98-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2de98-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2de98-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2de98-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2de98-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2de98-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2de98-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="2de98-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2de98-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="2de98-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2de98-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2de98-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2de98-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2de98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2de98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2de98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2de98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2de98-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2de98-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2de98-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2de98-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2de98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2de98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2de98-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2de98-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2de98-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="2de98-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="2de98-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2de98-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="2de98-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2de98-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="2de98-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2de98-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

1. <span data-ttu-id="2de98-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2de98-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="2de98-157">a.</span><span class="sxs-lookup"><span data-stu-id="2de98-157">a.</span></span> <span data-ttu-id="2de98-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="2de98-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="2de98-159">b.</span><span class="sxs-lookup"><span data-stu-id="2de98-159">b.</span></span> <span data-ttu-id="2de98-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="2de98-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="2de98-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2de98-161">These values are not real.</span></span> <span data-ttu-id="2de98-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="2de98-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2de98-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="2de98-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
1. <span data-ttu-id="2de98-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2de98-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

1. <span data-ttu-id="2de98-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2de98-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/directions-microsoft-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="2de98-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2de98-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="2de98-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span><span class="sxs-lookup"><span data-stu-id="2de98-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="2de98-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2de98-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="2de98-171">You will receive a notification when single sign-on has been enabled.</span><span class="sxs-lookup"><span data-stu-id="2de98-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="2de98-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2de98-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2de98-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2de98-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2de98-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2de98-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2de98-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2de98-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="2de98-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2de98-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2de98-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2de98-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2de98-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2de98-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="2de98-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2de98-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="2de98-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2de98-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="2de98-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2de98-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2de98-187">a.</span><span class="sxs-lookup"><span data-stu-id="2de98-187">a.</span></span> <span data-ttu-id="2de98-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2de98-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2de98-189">b.</span><span class="sxs-lookup"><span data-stu-id="2de98-189">b.</span></span> <span data-ttu-id="2de98-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2de98-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2de98-191">c.</span><span class="sxs-lookup"><span data-stu-id="2de98-191">c.</span></span> <span data-ttu-id="2de98-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2de98-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2de98-193">d.</span><span class="sxs-lookup"><span data-stu-id="2de98-193">d.</span></span> <span data-ttu-id="2de98-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2de98-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="2de98-195">Creating a Directions on Microsoft test user</span><span class="sxs-lookup"><span data-stu-id="2de98-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="2de98-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2de98-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="2de98-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="2de98-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="2de98-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2de98-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2de98-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2de98-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2de98-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2de98-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Assign User][200] 

<span data-ttu-id="2de98-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2de98-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="2de98-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2de98-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2de98-205">In the applications list, select **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2de98-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Configure Single Sign-On](./media/directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

1. <span data-ttu-id="2de98-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2de98-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2de98-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2de98-209">Click **Add** button.</span></span> <span data-ttu-id="2de98-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2de98-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2de98-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2de98-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2de98-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2de98-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2de98-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2de98-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2de98-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2de98-215">Testing single sign-on</span></span>

<span data-ttu-id="2de98-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2de98-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="2de98-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span><span class="sxs-lookup"><span data-stu-id="2de98-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="2de98-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2de98-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2de98-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2de98-219">Additional resources</span></span>

* [<span data-ttu-id="2de98-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2de98-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2de98-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2de98-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/directions-microsoft-tutorial/tutorial_general_203.png

