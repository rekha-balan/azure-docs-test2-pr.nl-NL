---
title: 'Tutorial: Azure Active Directory integration with Bambu by Sprout Social | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bambu by Sprout Social.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 1240049fd84633365aa55cd07dfb0e4ef75d24d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870026"
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="a7990-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="a7990-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="a7990-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7990-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7990-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a7990-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7990-106">You can control in Azure AD who has access to Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="a7990-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="a7990-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a7990-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7990-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a7990-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7990-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a7990-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7990-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7990-110">Prerequisites</span></span>

<span data-ttu-id="a7990-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a7990-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="a7990-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a7990-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7990-113">A Bambu by Sprout Social single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a7990-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7990-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a7990-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7990-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a7990-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7990-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="a7990-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a7990-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7990-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7990-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a7990-118">Scenario description</span></span>
<span data-ttu-id="a7990-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a7990-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7990-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7990-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7990-121">Adding Bambu by Sprout Social from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7990-121">Adding Bambu by Sprout Social from the gallery</span></span>
1. <span data-ttu-id="a7990-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7990-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="a7990-123">Adding Bambu by Sprout Social from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7990-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="a7990-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a7990-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7990-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7990-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7990-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7990-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a7990-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a7990-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7990-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7990-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a7990-131">Click **New application** button on the top of the dialog to add new application.</span><span class="sxs-lookup"><span data-stu-id="a7990-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a7990-133">In the search box, type **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="a7990-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

1. <span data-ttu-id="a7990-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a7990-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7990-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7990-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7990-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7990-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7990-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7990-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="a7990-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a7990-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="a7990-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="a7990-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="a7990-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7990-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7990-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a7990-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a7990-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7990-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a7990-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="a7990-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="a7990-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7990-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a7990-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a7990-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7990-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7990-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7990-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span><span class="sxs-lookup"><span data-stu-id="a7990-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="a7990-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7990-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="a7990-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7990-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a7990-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="a7990-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

1. <span data-ttu-id="a7990-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="a7990-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

1. <span data-ttu-id="a7990-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a7990-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

1. <span data-ttu-id="a7990-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a7990-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a7990-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a7990-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a7990-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a7990-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

1. <span data-ttu-id="a7990-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="a7990-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="a7990-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a7990-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a7990-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a7990-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7990-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a7990-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7990-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7990-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7990-169">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7990-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7990-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7990-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a7990-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7990-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7990-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7990-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a7990-175">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="a7990-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a7990-177">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7990-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a7990-179">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7990-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7990-181">a.</span><span class="sxs-lookup"><span data-stu-id="a7990-181">a.</span></span> <span data-ttu-id="a7990-182">In the **Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7990-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="a7990-183">b.</span><span class="sxs-lookup"><span data-stu-id="a7990-183">b.</span></span> <span data-ttu-id="a7990-184">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7990-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a7990-185">c.</span><span class="sxs-lookup"><span data-stu-id="a7990-185">c.</span></span> <span data-ttu-id="a7990-186">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a7990-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7990-187">d.</span><span class="sxs-lookup"><span data-stu-id="a7990-187">d.</span></span> <span data-ttu-id="a7990-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a7990-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="a7990-189">Creating a Bambu by Sprout Social test user</span><span class="sxs-lookup"><span data-stu-id="a7990-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="a7990-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="a7990-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7990-191">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7990-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7990-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="a7990-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Assign User][200] 

<span data-ttu-id="a7990-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7990-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="a7990-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7990-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a7990-197">In the applications list, select **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="a7990-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configure Single Sign-On](./media/bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

1. <span data-ttu-id="a7990-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a7990-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a7990-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a7990-201">Click **Add** button.</span></span> <span data-ttu-id="a7990-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7990-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a7990-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a7990-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a7990-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7990-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a7990-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7990-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7990-207">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7990-207">Testing single sign-on</span></span>

<span data-ttu-id="a7990-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a7990-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7990-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span><span class="sxs-lookup"><span data-stu-id="a7990-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="a7990-210">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7990-210">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7990-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a7990-211">Additional resources</span></span>

* [<span data-ttu-id="a7990-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7990-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a7990-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7990-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/bambubysproutsocial-tutorial/tutorial_general_203.png
