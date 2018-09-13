---
title: 'Tutorial: Azure Active Directory integration with SAP NetWeaver | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAP NetWeaver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b773380a21e0c47a1e1519e592aa0ddd5e6388fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867023"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="8a0ca-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="8a0ca-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="8a0ca-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a0ca-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a0ca-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a0ca-106">You can control in Azure AD who has access to SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="8a0ca-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="8a0ca-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8a0ca-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a0ca-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8a0ca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a0ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8a0ca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8a0ca-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a0ca-110">Prerequisites</span></span>

<span data-ttu-id="8a0ca-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="8a0ca-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8a0ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a0ca-113">An SAP NetWeaver single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8a0ca-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a0ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a0ca-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a0ca-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a0ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a0ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a0ca-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8a0ca-118">Scenario description</span></span>
<span data-ttu-id="8a0ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a0ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a0ca-121">Adding SAP NetWeaver from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a0ca-121">Adding SAP NetWeaver from the gallery</span></span>
1. <span data-ttu-id="8a0ca-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a0ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="8a0ca-123">Adding SAP NetWeaver from the gallery</span><span class="sxs-lookup"><span data-stu-id="8a0ca-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="8a0ca-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a0ca-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a0ca-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a0ca-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8a0ca-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a0ca-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8a0ca-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8a0ca-133">In the search box, type **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

1. <span data-ttu-id="8a0ca-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a0ca-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a0ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a0ca-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8a0ca-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a0ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="8a0ca-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="8a0ca-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="8a0ca-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a0ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8a0ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8a0ca-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8a0ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8a0ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a0ca-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a0ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a0ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="8a0ca-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a0ca-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="8a0ca-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8a0ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

1. <span data-ttu-id="8a0ca-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="8a0ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-157">a.</span></span> <span data-ttu-id="8a0ca-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="8a0ca-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="8a0ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-159">b.</span></span> <span data-ttu-id="8a0ca-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="8a0ca-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="8a0ca-161">c.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-161">c.</span></span> <span data-ttu-id="8a0ca-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="8a0ca-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8a0ca-163">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-163">These values are not the real.</span></span> <span data-ttu-id="8a0ca-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8a0ca-165">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="8a0ca-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

1. <span data-ttu-id="8a0ca-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

1. <span data-ttu-id="8a0ca-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="8a0ca-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8a0ca-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8a0ca-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

1. <span data-ttu-id="8a0ca-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="8a0ca-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="8a0ca-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8a0ca-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a0ca-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a0ca-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a0ca-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a0ca-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a0ca-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a0ca-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8a0ca-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a0ca-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a0ca-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8a0ca-184">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8a0ca-186">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8a0ca-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a0ca-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a0ca-190">a.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-190">a.</span></span> <span data-ttu-id="8a0ca-191">In the **Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="8a0ca-192">b.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-192">b.</span></span> <span data-ttu-id="8a0ca-193">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="8a0ca-194">c.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-194">c.</span></span> <span data-ttu-id="8a0ca-195">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a0ca-196">d.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-196">d.</span></span> <span data-ttu-id="8a0ca-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="8a0ca-198">Creating an SAP NetWeaver test user</span><span class="sxs-lookup"><span data-stu-id="8a0ca-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="8a0ca-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="8a0ca-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a0ca-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8a0ca-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a0ca-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Assign User][200] 

<span data-ttu-id="8a0ca-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8a0ca-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="8a0ca-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8a0ca-207">In the applications list, select **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Configure Single Sign-On](./media/sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

1. <span data-ttu-id="8a0ca-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8a0ca-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-211">Click **Add** button.</span></span> <span data-ttu-id="8a0ca-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8a0ca-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8a0ca-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8a0ca-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a0ca-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8a0ca-217">Testing single sign-on</span></span>

<span data-ttu-id="8a0ca-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a0ca-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span><span class="sxs-lookup"><span data-stu-id="8a0ca-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a0ca-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8a0ca-220">Additional resources</span></span>

* [<span data-ttu-id="8a0ca-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a0ca-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8a0ca-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a0ca-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/sap-netweaver-tutorial/tutorial_general_203.png

