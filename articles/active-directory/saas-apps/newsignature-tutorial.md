---
title: 'Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cloud Management Portal for Microsoft Azure.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0cd14a308758701e207e0b1ee6d3591c4b0347bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871005"
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="63d69-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="63d69-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="63d69-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63d69-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63d69-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="63d69-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63d69-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="63d69-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="63d69-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="63d69-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63d69-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="63d69-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="63d69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="63d69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63d69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63d69-110">Prerequisites</span></span>

<span data-ttu-id="63d69-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="63d69-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="63d69-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="63d69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63d69-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="63d69-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63d69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="63d69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63d69-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="63d69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63d69-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="63d69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63d69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63d69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63d69-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="63d69-118">Scenario description</span></span>
<span data-ttu-id="63d69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="63d69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63d69-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="63d69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63d69-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span><span class="sxs-lookup"><span data-stu-id="63d69-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
1. <span data-ttu-id="63d69-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63d69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="63d69-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span><span class="sxs-lookup"><span data-stu-id="63d69-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="63d69-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="63d69-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63d69-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63d69-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63d69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="63d69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="63d69-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="63d69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63d69-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="63d69-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="63d69-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="63d69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="63d69-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="63d69-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Creating an Azure AD test user](./media/newsignature-tutorial/tutorial_newsignature_search.png)

1. <span data-ttu-id="63d69-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="63d69-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63d69-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63d69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63d69-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63d69-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63d69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63d69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="63d69-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span><span class="sxs-lookup"><span data-stu-id="63d69-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="63d69-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="63d69-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63d69-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="63d69-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63d69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="63d69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="63d69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63d69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="63d69-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="63d69-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="63d69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="63d69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="63d69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="63d69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63d69-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63d69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63d69-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span><span class="sxs-lookup"><span data-stu-id="63d69-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="63d69-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63d69-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="63d69-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="63d69-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="63d69-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="63d69-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_newsignature_samlbase.png)

1. <span data-ttu-id="63d69-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63d69-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="63d69-157">a.</span><span class="sxs-lookup"><span data-stu-id="63d69-157">a.</span></span> <span data-ttu-id="63d69-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="63d69-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="63d69-159">b.</span><span class="sxs-lookup"><span data-stu-id="63d69-159">b.</span></span> <span data-ttu-id="63d69-160">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="63d69-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="63d69-161">c.</span><span class="sxs-lookup"><span data-stu-id="63d69-161">c.</span></span> <span data-ttu-id="63d69-162">In the **Reply URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="63d69-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="63d69-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="63d69-163">These values are not real.</span></span> <span data-ttu-id="63d69-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="63d69-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="63d69-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="63d69-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
1. <span data-ttu-id="63d69-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="63d69-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_newsignature_certificate.png) 

1. <span data-ttu-id="63d69-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="63d69-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="63d69-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="63d69-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="63d69-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="63d69-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_newsignature_configure.png) 

1. <span data-ttu-id="63d69-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="63d69-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="63d69-174">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="63d69-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="63d69-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="63d69-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63d69-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="63d69-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63d69-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63d69-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63d69-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63d69-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="63d69-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63d69-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="63d69-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63d69-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63d69-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="63d69-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/newsignature-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="63d69-184">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="63d69-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/newsignature-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="63d69-186">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="63d69-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/newsignature-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="63d69-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63d69-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63d69-190">a.</span><span class="sxs-lookup"><span data-stu-id="63d69-190">a.</span></span> <span data-ttu-id="63d69-191">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63d69-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63d69-192">b.</span><span class="sxs-lookup"><span data-stu-id="63d69-192">b.</span></span> <span data-ttu-id="63d69-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63d69-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63d69-194">c.</span><span class="sxs-lookup"><span data-stu-id="63d69-194">c.</span></span> <span data-ttu-id="63d69-195">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="63d69-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63d69-196">d.</span><span class="sxs-lookup"><span data-stu-id="63d69-196">d.</span></span> <span data-ttu-id="63d69-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="63d69-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="63d69-198">Creating a Cloud Management Portal for Microsoft Azure test user</span><span class="sxs-lookup"><span data-stu-id="63d69-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="63d69-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="63d69-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="63d69-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span><span class="sxs-lookup"><span data-stu-id="63d69-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63d69-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63d69-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="63d69-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="63d69-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Assign User][200] 

<span data-ttu-id="63d69-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63d69-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="63d69-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="63d69-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="63d69-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="63d69-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configure Single Sign-On](./media/newsignature-tutorial/tutorial_newsignature_app.png) 

1. <span data-ttu-id="63d69-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="63d69-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="63d69-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="63d69-211">Click **Add** button.</span></span> <span data-ttu-id="63d69-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="63d69-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="63d69-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="63d69-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="63d69-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="63d69-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="63d69-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="63d69-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63d69-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="63d69-217">Testing single sign-on</span></span>

<span data-ttu-id="63d69-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="63d69-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="63d69-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span><span class="sxs-lookup"><span data-stu-id="63d69-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="63d69-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="63d69-220">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63d69-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="63d69-221">Additional resources</span></span>

* [<span data-ttu-id="63d69-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63d69-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="63d69-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63d69-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/newsignature-tutorial/tutorial_general_01.png
[2]: ./media/newsignature-tutorial/tutorial_general_02.png
[3]: ./media/newsignature-tutorial/tutorial_general_03.png
[4]: ./media/newsignature-tutorial/tutorial_general_04.png

[100]: ./media/newsignature-tutorial/tutorial_general_100.png

[200]: ./media/newsignature-tutorial/tutorial_general_200.png
[201]: ./media/newsignature-tutorial/tutorial_general_201.png
[202]: ./media/newsignature-tutorial/tutorial_general_202.png
[203]: ./media/newsignature-tutorial/tutorial_general_203.png

