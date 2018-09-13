---
title: 'Tutorial: Azure Active Directory integration with SCC LifeCycle | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SCC LifeCycle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e24ef84ddbb4c3d1007f420f46c1f28888e2016e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856883"
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="a7940-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="a7940-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="a7940-104">In this tutorial, you learn how to integrate SCC LifeCycle with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7940-104">In this tutorial, you learn how to integrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7940-105">Integrating SCC LifeCycle with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a7940-105">Integrating SCC LifeCycle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7940-106">You can control in Azure AD who has access to SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="a7940-106">You can control in Azure AD who has access to SCC LifeCycle</span></span>
- <span data-ttu-id="a7940-107">You can enable your users to automatically get signed-on to SCC LifeCycle (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a7940-107">You can enable your users to automatically get signed-on to SCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7940-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a7940-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7940-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a7940-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7940-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7940-110">Prerequisites</span></span>

<span data-ttu-id="a7940-111">To configure Azure AD integration with SCC LifeCycle, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a7940-111">To configure Azure AD integration with SCC LifeCycle, you need the following items:</span></span>

- <span data-ttu-id="a7940-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a7940-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7940-113">An SCC LifeCycle single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a7940-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7940-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a7940-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7940-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a7940-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7940-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a7940-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7940-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7940-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7940-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a7940-118">Scenario description</span></span>
<span data-ttu-id="a7940-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a7940-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7940-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7940-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7940-121">Adding SCC LifeCycle from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7940-121">Adding SCC LifeCycle from the gallery</span></span>
1. <span data-ttu-id="a7940-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7940-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-the-gallery"></a><span data-ttu-id="a7940-123">Adding SCC LifeCycle from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7940-123">Adding SCC LifeCycle from the gallery</span></span>
<span data-ttu-id="a7940-124">To configure the integration of SCC LifeCycle into Azure AD, you need to add SCC LifeCycle from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a7940-124">To configure the integration of SCC LifeCycle into Azure AD, you need to add SCC LifeCycle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7940-125">**To add SCC LifeCycle from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7940-125">**To add SCC LifeCycle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7940-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7940-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a7940-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a7940-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7940-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7940-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a7940-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a7940-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a7940-133">In the search box, type **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="a7940-133">In the search box, type **SCC LifeCycle**.</span></span>

    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/tutorial_scclifecycle_search.png)

1. <span data-ttu-id="a7940-135">In the results panel, select **SCC LifeCycle**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a7940-135">In the results panel, select **SCC LifeCycle**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7940-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7940-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a7940-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a7940-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7940-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SCC LifeCycle is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7940-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SCC LifeCycle is to a user in Azure AD.</span></span> <span data-ttu-id="a7940-140">In other words, a link relationship between an Azure AD user and the related user in SCC LifeCycle needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a7940-140">In other words, a link relationship between an Azure AD user and the related user in SCC LifeCycle needs to be established.</span></span>

<span data-ttu-id="a7940-141">In SCC LifeCycle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a7940-141">In SCC LifeCycle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7940-142">To configure and test Azure AD single sign-on with SCC LifeCycle, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7940-142">To configure and test Azure AD single sign-on with SCC LifeCycle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7940-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a7940-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a7940-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7940-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a7940-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - to have a counterpart of Britta Simon in SCC LifeCycle that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a7940-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - to have a counterpart of Britta Simon in SCC LifeCycle that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a7940-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7940-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a7940-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a7940-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7940-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7940-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7940-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SCC LifeCycle application.</span><span class="sxs-lookup"><span data-stu-id="a7940-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="a7940-150">**To configure Azure AD single sign-on with SCC LifeCycle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7940-150">**To configure Azure AD single sign-on with SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="a7940-151">In the Azure portal, on the **SCC LifeCycle** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7940-151">In the Azure portal, on the **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a7940-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7940-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

1. <span data-ttu-id="a7940-155">On the **SCC LifeCycle Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7940-155">On the **SCC LifeCycle Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="a7940-157">a.</span><span class="sxs-lookup"><span data-stu-id="a7940-157">a.</span></span> <span data-ttu-id="a7940-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="a7940-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="a7940-159">b.</span><span class="sxs-lookup"><span data-stu-id="a7940-159">b.</span></span> <span data-ttu-id="a7940-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a7940-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="a7940-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a7940-161">These values are not real.</span></span> <span data-ttu-id="a7940-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a7940-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a7940-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a7940-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) to get these values.</span></span> 
 
1. <span data-ttu-id="a7940-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a7940-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

1. <span data-ttu-id="a7940-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a7940-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/scclifecycle-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a7940-168">To configure single sign-on on **SCC LifeCycle** side, you need to send the downloaded **Metadata XML** to [SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="a7940-168">To configure single sign-on on **SCC LifeCycle** side, you need to send the downloaded **Metadata XML** to [SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="a7940-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a7940-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="a7940-170">Single sign-on has to be enabled by the SCC LifeCycle support team.</span><span class="sxs-lookup"><span data-stu-id="a7940-170">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>

> [!TIP]
> <span data-ttu-id="a7940-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a7940-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7940-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a7940-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7940-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7940-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7940-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7940-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7940-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7940-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a7940-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7940-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7940-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7940-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a7940-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a7940-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a7940-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a7940-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a7940-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7940-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7940-186">a.</span><span class="sxs-lookup"><span data-stu-id="a7940-186">a.</span></span> <span data-ttu-id="a7940-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7940-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7940-188">b.</span><span class="sxs-lookup"><span data-stu-id="a7940-188">b.</span></span> <span data-ttu-id="a7940-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7940-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7940-190">c.</span><span class="sxs-lookup"><span data-stu-id="a7940-190">c.</span></span> <span data-ttu-id="a7940-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a7940-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7940-192">d.</span><span class="sxs-lookup"><span data-stu-id="a7940-192">d.</span></span> <span data-ttu-id="a7940-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a7940-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="a7940-194">Creating an SCC LifeCycle test user</span><span class="sxs-lookup"><span data-stu-id="a7940-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="a7940-195">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="a7940-195">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="a7940-196">There is no action item for you to configure user provisioning to SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="a7940-196">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="a7940-197">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span><span class="sxs-lookup"><span data-stu-id="a7940-197">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="a7940-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a7940-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7940-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7940-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7940-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="a7940-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SCC LifeCycle.</span></span>

![Assign User][200] 

<span data-ttu-id="a7940-202">**To assign Britta Simon to SCC LifeCycle, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7940-202">**To assign Britta Simon to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="a7940-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications.**</span><span class="sxs-lookup"><span data-stu-id="a7940-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications.**</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a7940-205">In the applications list, select **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="a7940-205">In the applications list, select **SCC LifeCycle**.</span></span>

    ![Configure Single Sign-On](./media/scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

1. <span data-ttu-id="a7940-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a7940-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a7940-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a7940-209">Click **Add** button.</span></span> <span data-ttu-id="a7940-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7940-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a7940-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a7940-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a7940-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7940-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a7940-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7940-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7940-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7940-215">Testing single sign-on</span></span>

<span data-ttu-id="a7940-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a7940-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7940-217">When you click the SCC LifeCycle tile in the Access Panel, you should get automatically signed-on to SCC LifeCycle application.</span><span class="sxs-lookup"><span data-stu-id="a7940-217">When you click the SCC LifeCycle tile in the Access Panel, you should get automatically signed-on to SCC LifeCycle application.</span></span>
<span data-ttu-id="a7940-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7940-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7940-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a7940-219">Additional resources</span></span>

* [<span data-ttu-id="a7940-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7940-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a7940-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7940-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/scclifecycle-tutorial/tutorial_general_203.png

