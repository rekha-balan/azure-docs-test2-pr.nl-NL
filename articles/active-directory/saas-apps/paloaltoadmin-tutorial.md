---
title: 'Tutorial: Azure Active Directory integration with Palo Alto Networks - Admin UI | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Palo Alto Networks - Admin UI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a826eaec-15af-4c85-8855-8a3374d1efb9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: jeedes
ms.openlocfilehash: fed368c0df265495d9fee764f86825957fae8bab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868620"
---
# <a name="integrate-azure-active-directory-with-palo-alto-networks---admin-ui"></a><span data-ttu-id="68dac-103">Integrate Azure Active Directory with Palo Alto Networks - Admin UI</span><span class="sxs-lookup"><span data-stu-id="68dac-103">Integrate Azure Active Directory with Palo Alto Networks - Admin UI</span></span>

<span data-ttu-id="68dac-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Palo Alto Networks - Admin UI.</span><span class="sxs-lookup"><span data-stu-id="68dac-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Palo Alto Networks - Admin UI.</span></span>

<span data-ttu-id="68dac-105">By integrating Azure AD with Palo Alto Networks - Admin UI, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="68dac-105">By integrating Azure AD with Palo Alto Networks - Admin UI, you get the following benefits:</span></span>

- <span data-ttu-id="68dac-106">You can control in Azure AD who has access to Palo Alto Networks - Admin UI.</span><span class="sxs-lookup"><span data-stu-id="68dac-106">You can control in Azure AD who has access to Palo Alto Networks - Admin UI.</span></span>
- <span data-ttu-id="68dac-107">You can enable your users to get signed in automatically to Palo Alto Networks - Admin UI (single sign-on, or SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="68dac-107">You can enable your users to get signed in automatically to Palo Alto Networks - Admin UI (single sign-on, or SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="68dac-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="68dac-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="68dac-109">To learn about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="68dac-109">To learn about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68dac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="68dac-110">Prerequisites</span></span>

<span data-ttu-id="68dac-111">To configure Azure AD integration with Palo Alto Networks - Admin UI, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="68dac-111">To configure Azure AD integration with Palo Alto Networks - Admin UI, you need the following items:</span></span>

- <span data-ttu-id="68dac-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="68dac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68dac-113">A Palo Alto Networks Next-Generation Firewall or Panorama (centralized management system for the firewalls)</span><span class="sxs-lookup"><span data-stu-id="68dac-113">A Palo Alto Networks Next-Generation Firewall or Panorama (centralized management system for the firewalls)</span></span>

> [!NOTE]
> <span data-ttu-id="68dac-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span><span class="sxs-lookup"><span data-stu-id="68dac-114">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span></span>

<span data-ttu-id="68dac-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="68dac-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="68dac-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="68dac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68dac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68dac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68dac-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="68dac-118">Scenario description</span></span>
<span data-ttu-id="68dac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="68dac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="68dac-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="68dac-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="68dac-121">Adding Palo Alto Networks - Admin UI from the gallery</span><span class="sxs-lookup"><span data-stu-id="68dac-121">Adding Palo Alto Networks - Admin UI from the gallery</span></span>
* <span data-ttu-id="68dac-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68dac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-palo-alto-networks---admin-ui-from-the-gallery"></a><span data-ttu-id="68dac-123">Add Palo Alto Networks - Admin UI from the gallery</span><span class="sxs-lookup"><span data-stu-id="68dac-123">Add Palo Alto Networks - Admin UI from the gallery</span></span>
<span data-ttu-id="68dac-124">To configure the integration of Azure AD with Palo Alto Networks - Admin UI, add Palo Alto Networks - Admin UI from the gallery to your list of managed SaaS apps by doing the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-124">To configure the integration of Azure AD with Palo Alto Networks - Admin UI, add Palo Alto Networks - Admin UI from the gallery to your list of managed SaaS apps by doing the following:</span></span>

1. <span data-ttu-id="68dac-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68dac-125">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="68dac-127">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="68dac-127">Select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" window][2]
    
1. <span data-ttu-id="68dac-129">To add a new application, select the **New application** button at the top of window.</span><span class="sxs-lookup"><span data-stu-id="68dac-129">To add a new application, select the **New application** button at the top of window.</span></span>

    ![The "New application" button][3]

1. <span data-ttu-id="68dac-131">In the search box, type **Palo Alto Networks - Admin UI**, select **Palo Alto Networks - Admin UI** in the results list, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="68dac-131">In the search box, type **Palo Alto Networks - Admin UI**, select **Palo Alto Networks - Admin UI** in the results list, and then select **Add**.</span></span>

    ![Palo Alto Networks - Admin UI in the results list](./media/paloaltoadmin-tutorial/tutorial_step4-add-from-the-gallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="68dac-133">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68dac-133">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="68dac-134">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Admin UI, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="68dac-134">In this section, you configure and test Azure AD single sign-on with Palo Alto Networks - Admin UI, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68dac-135">For single sign-on to work, Azure AD needs to identify the Palo Alto Networks - Admin UI user and its counterpart in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68dac-135">For single sign-on to work, Azure AD needs to identify the Palo Alto Networks - Admin UI user and its counterpart in Azure AD.</span></span> <span data-ttu-id="68dac-136">In other words, a link relationship between an Azure AD user and the same user in Palo Alto Networks - Admin UI must be established.</span><span class="sxs-lookup"><span data-stu-id="68dac-136">In other words, a link relationship between an Azure AD user and the same user in Palo Alto Networks - Admin UI must be established.</span></span>

<span data-ttu-id="68dac-137">To establish the link relationship, assign as the Palo Alto Networks - Admin UI *Username* the value of the *user name* in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68dac-137">To establish the link relationship, assign as the Palo Alto Networks - Admin UI *Username* the value of the *user name* in Azure AD.</span></span>

<span data-ttu-id="68dac-138">To configure and test Azure AD single sign-on with Palo Alto Networks - Admin UI, complete the building blocks in the next five sections.</span><span class="sxs-lookup"><span data-stu-id="68dac-138">To configure and test Azure AD single sign-on with Palo Alto Networks - Admin UI, complete the building blocks in the next five sections.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="68dac-139">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="68dac-139">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="68dac-140">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Admin UI application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-140">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Palo Alto Networks - Admin UI application by doing the following:</span></span>

1. <span data-ttu-id="68dac-141">In the Azure portal, on the **Palo Alto Networks - Admin UI** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="68dac-141">In the Azure portal, on the **Palo Alto Networks - Admin UI** application integration page, select **Single sign-on**.</span></span>

    ![The "Single sign-on" link][4]

1. <span data-ttu-id="68dac-143">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="68dac-143">In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.</span></span>
 
    ![The "Single sign-on" window](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_samlbase.png)

1. <span data-ttu-id="68dac-145">Under **Palo Alto Networks - Admin UI Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-145">Under **Palo Alto Networks - Admin UI Domain and URLs**, do the following:</span></span>

    !["Palo Alto Networks - Admin UI Domain and URLs" single sign-on information](./media/paloaltoadmin-tutorial/tutorial_general_show_advanced_url.png)
    
    <span data-ttu-id="68dac-147">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-147">a.</span></span> <span data-ttu-id="68dac-148">In the **Sign-on URL** box, type a URL in the following format: *https://\<Customer Firewall FQDN>/php/login.php*.</span><span class="sxs-lookup"><span data-stu-id="68dac-148">In the **Sign-on URL** box, type a URL in the following format: *https://\<Customer Firewall FQDN>/php/login.php*.</span></span>

    <span data-ttu-id="68dac-149">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-149">b.</span></span> <span data-ttu-id="68dac-150">In the **Identifier** box, type a URL in the following format: *https://\<Customer Firewall FQDN>:443/SAML20/SP*.</span><span class="sxs-lookup"><span data-stu-id="68dac-150">In the **Identifier** box, type a URL in the following format: *https://\<Customer Firewall FQDN>:443/SAML20/SP*.</span></span>
    
    <span data-ttu-id="68dac-151">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-151">c.</span></span> <span data-ttu-id="68dac-152">In the **Reply URL** box, type the Assertion Consumer Service (ACS) URL in the following format: *https://\<Customer Firewall FQDN>:443/SAML20/SP/ACS*.</span><span class="sxs-lookup"><span data-stu-id="68dac-152">In the **Reply URL** box, type the Assertion Consumer Service (ACS) URL in the following format: *https://\<Customer Firewall FQDN>:443/SAML20/SP/ACS*.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="68dac-153">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="68dac-153">The preceding values are not real.</span></span> <span data-ttu-id="68dac-154">Update them with the actual sign-on URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="68dac-154">Update them with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="68dac-155">To obtain the values, contact [Palo Alto Networks - Admin UI Client support team](https://support.paloaltonetworks.com/support).</span><span class="sxs-lookup"><span data-stu-id="68dac-155">To obtain the values, contact [Palo Alto Networks - Admin UI Client support team](https://support.paloaltonetworks.com/support).</span></span> 
 
1. <span data-ttu-id="68dac-156">Because the Palo Alto Networks - Admin UI application expects the SAML assertions in a specific format, configure the claims as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="68dac-156">Because the Palo Alto Networks - Admin UI application expects the SAML assertions in a specific format, configure the claims as shown in the following image.</span></span> <span data-ttu-id="68dac-157">Manage the attribute values in the **User Attributes** section of the **Application Integration** page by doing the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-157">Manage the attribute values in the **User Attributes** section of the **Application Integration** page by doing the following:</span></span>
    
    ![The SAML Token Attributes list](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_attribute.png)
    
   > [!NOTE]
   > <span data-ttu-id="68dac-159">Because the attribute values are examples only, map the appropriate values for *username* and *adminrole*.</span><span class="sxs-lookup"><span data-stu-id="68dac-159">Because the attribute values are examples only, map the appropriate values for *username* and *adminrole*.</span></span> <span data-ttu-id="68dac-160">There is another optional attribute, *accessdomain*, which is used to restrict admin access to specific virtual systems on the firewall.</span><span class="sxs-lookup"><span data-stu-id="68dac-160">There is another optional attribute, *accessdomain*, which is used to restrict admin access to specific virtual systems on the firewall.</span></span>
   >
        
    | <span data-ttu-id="68dac-161">Attribute name</span><span class="sxs-lookup"><span data-stu-id="68dac-161">Attribute name</span></span> | <span data-ttu-id="68dac-162">Attribute value</span><span class="sxs-lookup"><span data-stu-id="68dac-162">Attribute value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="68dac-163">username</span><span class="sxs-lookup"><span data-stu-id="68dac-163">username</span></span> | <span data-ttu-id="68dac-164">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="68dac-164">user.userprincipalname</span></span> |
    | <span data-ttu-id="68dac-165">adminrole</span><span class="sxs-lookup"><span data-stu-id="68dac-165">adminrole</span></span> | <span data-ttu-id="68dac-166">customadmin</span><span class="sxs-lookup"><span data-stu-id="68dac-166">customadmin</span></span> |

    <span data-ttu-id="68dac-167">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-167">a.</span></span> <span data-ttu-id="68dac-168">Select **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="68dac-168">Select **Add attribute**.</span></span>  
    
    ![The "Add attribute" button](./media/paloaltoadmin-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="68dac-170">The **Add Attribute** window opens.</span><span class="sxs-lookup"><span data-stu-id="68dac-170">The **Add Attribute** window opens.</span></span>

    ![The "Add attribute" window](./media/paloaltoadmin-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="68dac-172">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-172">b.</span></span> <span data-ttu-id="68dac-173">In the **Name** box, type the attribute name that's shown for that row.</span><span class="sxs-lookup"><span data-stu-id="68dac-173">In the **Name** box, type the attribute name that's shown for that row.</span></span>
    
    <span data-ttu-id="68dac-174">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-174">c.</span></span> <span data-ttu-id="68dac-175">In the **Value** box, type the attribute value that's shown for that row.</span><span class="sxs-lookup"><span data-stu-id="68dac-175">In the **Value** box, type the attribute value that's shown for that row.</span></span>
    
    <span data-ttu-id="68dac-176">d.</span><span class="sxs-lookup"><span data-stu-id="68dac-176">d.</span></span> <span data-ttu-id="68dac-177">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="68dac-177">Select **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="68dac-178">For more information about the attributes, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="68dac-178">For more information about the attributes, see the following articles:</span></span>
    > * [<span data-ttu-id="68dac-179">Administrative role profile for Admin UI (adminrole)</span><span class="sxs-lookup"><span data-stu-id="68dac-179">Administrative role profile for Admin UI (adminrole)</span></span>](https://www.paloaltonetworks.com/documentation/80/pan-os/pan-os/firewall-administration/manage-firewall-administrators/configure-an-admin-role-profile)
    > * [<span data-ttu-id="68dac-180">Device access domain for Admin UI (accessdomain)</span><span class="sxs-lookup"><span data-stu-id="68dac-180">Device access domain for Admin UI (accessdomain)</span></span>](https://www.paloaltonetworks.com/documentation/80/pan-os/web-interface-help/device/device-access-domain)
    >

1. <span data-ttu-id="68dac-181">Under **SAML Signing Certificate**, select **Metadata XML**, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="68dac-181">Under **SAML Signing Certificate**, select **Metadata XML**, and then select **Save**.</span></span>

    ![The Metadata XML download link](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_certificate.png) 

    ![The Save button](./media/paloaltoadmin-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="68dac-184">Open the Palo Alto Networks Firewall Admin UI as an administrator in a new window.</span><span class="sxs-lookup"><span data-stu-id="68dac-184">Open the Palo Alto Networks Firewall Admin UI as an administrator in a new window.</span></span>

1. <span data-ttu-id="68dac-185">Select the **Device** tab.</span><span class="sxs-lookup"><span data-stu-id="68dac-185">Select the **Device** tab.</span></span>

    ![The Device tab](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin1.png)

1. <span data-ttu-id="68dac-187">In the left pane, select **SAML Identity Provider**, and then select **Import** to import the metadata file.</span><span class="sxs-lookup"><span data-stu-id="68dac-187">In the left pane, select **SAML Identity Provider**, and then select **Import** to import the metadata file.</span></span>

    ![The Import metadata file button](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin2.png)

1. <span data-ttu-id="68dac-189">In the **SAML Identify Provider Server Profile Import** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-189">In the **SAML Identify Provider Server Profile Import** window, do the following:</span></span>

    ![The "SAML Identify Provider Server Profile Import" window](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_idp.png)

    <span data-ttu-id="68dac-191">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-191">a.</span></span> <span data-ttu-id="68dac-192">In the **Profile Name** box, provide a name (for example, **AzureAD Admin UI**).</span><span class="sxs-lookup"><span data-stu-id="68dac-192">In the **Profile Name** box, provide a name (for example, **AzureAD Admin UI**).</span></span>
    
    <span data-ttu-id="68dac-193">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-193">b.</span></span> <span data-ttu-id="68dac-194">Under **Identity Provider Metadata**, select **Browse**, and select the metadata.xml file that you downloaded earlier from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="68dac-194">Under **Identity Provider Metadata**, select **Browse**, and select the metadata.xml file that you downloaded earlier from the Azure portal.</span></span>
    
    <span data-ttu-id="68dac-195">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-195">c.</span></span> <span data-ttu-id="68dac-196">Clear the **Validate Identity Provider Certificate** check box.</span><span class="sxs-lookup"><span data-stu-id="68dac-196">Clear the **Validate Identity Provider Certificate** check box.</span></span>
    
    <span data-ttu-id="68dac-197">d.</span><span class="sxs-lookup"><span data-stu-id="68dac-197">d.</span></span> <span data-ttu-id="68dac-198">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="68dac-198">Select **OK**.</span></span>
    
    <span data-ttu-id="68dac-199">e.</span><span class="sxs-lookup"><span data-stu-id="68dac-199">e.</span></span> <span data-ttu-id="68dac-200">To commit the configurations on the firewall, select **Commit**.</span><span class="sxs-lookup"><span data-stu-id="68dac-200">To commit the configurations on the firewall, select **Commit**.</span></span>

1. <span data-ttu-id="68dac-201">In the left pane, select **SAML Identity Provider**, and then select the SAML Identity Provider Profile (for example, **AzureAD Admin UI**) that you created in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="68dac-201">In the left pane, select **SAML Identity Provider**, and then select the SAML Identity Provider Profile (for example, **AzureAD Admin UI**) that you created in the preceding step.</span></span> 

    ![The SAML Identity Provider Profile](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_idp_select.png)

1. <span data-ttu-id="68dac-203">In the **SAML Identity Provider Server Profile** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-203">In the **SAML Identity Provider Server Profile** window, do the following:</span></span>

    ![The "SAML Identity Provider Server Profile" window](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_slo.png)
  
    <span data-ttu-id="68dac-205">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-205">a.</span></span> <span data-ttu-id="68dac-206">In the **Identity Provider SLO URL** box, replace the previously imported SLO URL with the following URL: **https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0**.</span><span class="sxs-lookup"><span data-stu-id="68dac-206">In the **Identity Provider SLO URL** box, replace the previously imported SLO URL with the following URL: **https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0**.</span></span>
  
    <span data-ttu-id="68dac-207">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-207">b.</span></span> <span data-ttu-id="68dac-208">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="68dac-208">Select **OK**.</span></span>

1. <span data-ttu-id="68dac-209">On the Palo Alto Networks Firewall's Admin UI, select **Device**, and then select **Admin Roles**.</span><span class="sxs-lookup"><span data-stu-id="68dac-209">On the Palo Alto Networks Firewall's Admin UI, select **Device**, and then select **Admin Roles**.</span></span>

1. <span data-ttu-id="68dac-210">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="68dac-210">Select the **Add** button.</span></span> 

1. <span data-ttu-id="68dac-211">In the **Admin Role Profile** window, in the **Name** box, provide a name for the administrator role (for example, **fwadmin**).</span><span class="sxs-lookup"><span data-stu-id="68dac-211">In the **Admin Role Profile** window, in the **Name** box, provide a name for the administrator role (for example, **fwadmin**).</span></span>  
    <span data-ttu-id="68dac-212">The administrator role name should match the SAML Admin Role attribute name that was sent by the Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="68dac-212">The administrator role name should match the SAML Admin Role attribute name that was sent by the Identity Provider.</span></span> <span data-ttu-id="68dac-213">The administrator role name and value were created in step 4.</span><span class="sxs-lookup"><span data-stu-id="68dac-213">The administrator role name and value were created in step 4.</span></span>

    ![Configure Palo Alto Networks Admin Role](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_adminrole.png)
  
1. <span data-ttu-id="68dac-215">On the Firewall's Admin UI, select **Device**, and then select **Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="68dac-215">On the Firewall's Admin UI, select **Device**, and then select **Authentication Profile**.</span></span>

1. <span data-ttu-id="68dac-216">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="68dac-216">Select the **Add** button.</span></span> 

1. <span data-ttu-id="68dac-217">In the **Authentication Profile** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-217">In the **Authentication Profile** window, do the following:</span></span> 

    ![The "Authentication Profile" window](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_authentication_profile.png)

    <span data-ttu-id="68dac-219">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-219">a.</span></span> <span data-ttu-id="68dac-220">In the **Name** box, provide a name (for example, **AzureSAML_Admin_AuthProfile**).</span><span class="sxs-lookup"><span data-stu-id="68dac-220">In the **Name** box, provide a name (for example, **AzureSAML_Admin_AuthProfile**).</span></span>
    
    <span data-ttu-id="68dac-221">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-221">b.</span></span> <span data-ttu-id="68dac-222">In the **Type** drop-down list, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="68dac-222">In the **Type** drop-down list, select **SAML**.</span></span> 
   
    <span data-ttu-id="68dac-223">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-223">c.</span></span> <span data-ttu-id="68dac-224">In the **IdP Server Profile** drop-down list, select the appropriate SAML Identity Provider Server profile (for example, **AzureAD Admin UI**).</span><span class="sxs-lookup"><span data-stu-id="68dac-224">In the **IdP Server Profile** drop-down list, select the appropriate SAML Identity Provider Server profile (for example, **AzureAD Admin UI**).</span></span>
   
    <span data-ttu-id="68dac-225">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-225">c.</span></span> <span data-ttu-id="68dac-226">Select the **Enable Single Logout** check box.</span><span class="sxs-lookup"><span data-stu-id="68dac-226">Select the **Enable Single Logout** check box.</span></span>
    
    <span data-ttu-id="68dac-227">d.</span><span class="sxs-lookup"><span data-stu-id="68dac-227">d.</span></span> <span data-ttu-id="68dac-228">In the **Admin Role Attribute** box, enter the attribute name (for example, **adminrole**).</span><span class="sxs-lookup"><span data-stu-id="68dac-228">In the **Admin Role Attribute** box, enter the attribute name (for example, **adminrole**).</span></span> 
    
    <span data-ttu-id="68dac-229">e.</span><span class="sxs-lookup"><span data-stu-id="68dac-229">e.</span></span> <span data-ttu-id="68dac-230">Select the **Advanced** tab and then, under **Allow List**, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="68dac-230">Select the **Advanced** tab and then, under **Allow List**, select **Add**.</span></span> 
    
    ![The Add button on the Advanced tab](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_allowlist.png)
    
    <span data-ttu-id="68dac-232">f.</span><span class="sxs-lookup"><span data-stu-id="68dac-232">f.</span></span> <span data-ttu-id="68dac-233">Select the **All** check box, or select the users and groups that can authenticate with this profile.</span><span class="sxs-lookup"><span data-stu-id="68dac-233">Select the **All** check box, or select the users and groups that can authenticate with this profile.</span></span>  
    <span data-ttu-id="68dac-234">When a user authenticates, the firewall matches the associated username or group against the entries in this list.</span><span class="sxs-lookup"><span data-stu-id="68dac-234">When a user authenticates, the firewall matches the associated username or group against the entries in this list.</span></span> <span data-ttu-id="68dac-235">If you don’t add entries, no users can authenticate.</span><span class="sxs-lookup"><span data-stu-id="68dac-235">If you don’t add entries, no users can authenticate.</span></span>

    <span data-ttu-id="68dac-236">g.</span><span class="sxs-lookup"><span data-stu-id="68dac-236">g.</span></span> <span data-ttu-id="68dac-237">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="68dac-237">Select **OK**.</span></span>

1. <span data-ttu-id="68dac-238">To enable administrators to use SAML SSO by using Azure, select **Device** > **Setup**.</span><span class="sxs-lookup"><span data-stu-id="68dac-238">To enable administrators to use SAML SSO by using Azure, select **Device** > **Setup**.</span></span> <span data-ttu-id="68dac-239">In the **Setup** pane, select the **Management** tab and then, under **Authentication Settings**, select the **Settings** ("gear") button.</span><span class="sxs-lookup"><span data-stu-id="68dac-239">In the **Setup** pane, select the **Management** tab and then, under **Authentication Settings**, select the **Settings** ("gear") button.</span></span> 

 ![The Settings button](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_authsetup.png)

1. <span data-ttu-id="68dac-241">Select the SAML Authentication profile that you created in step 17 (for example, **AzureSAML_Admin_AuthProfile**).</span><span class="sxs-lookup"><span data-stu-id="68dac-241">Select the SAML Authentication profile that you created in step 17 (for example, **AzureSAML_Admin_AuthProfile**).</span></span>

 ![The Authentication Profile field](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_authsettings.png)

1. <span data-ttu-id="68dac-243">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="68dac-243">Select **OK**.</span></span>

1. <span data-ttu-id="68dac-244">To commit the configuration, select **Commit**.</span><span class="sxs-lookup"><span data-stu-id="68dac-244">To commit the configuration, select **Commit**.</span></span>


> [!TIP]
> <span data-ttu-id="68dac-245">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68dac-245">As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="68dac-246">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="68dac-246">After you've added the app in the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68dac-247">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="68dac-247">For more information about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="68dac-248">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="68dac-248">Create an Azure AD test user</span></span>

<span data-ttu-id="68dac-249">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-249">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Create an Azure AD test user][100]

1. <span data-ttu-id="68dac-251">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68dac-251">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory link](./media/paloaltoadmin-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="68dac-253">To display a list of current users, select **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="68dac-253">To display a list of current users, select **Users and groups** > **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/paloaltoadmin-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="68dac-255">At the top of the **All Users** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="68dac-255">At the top of the **All Users** window, select **Add**.</span></span>

    ![The Add button](./media/paloaltoadmin-tutorial/create_aaduser_03.png)
    
    <span data-ttu-id="68dac-257">The **User** window opens.</span><span class="sxs-lookup"><span data-stu-id="68dac-257">The **User** window opens.</span></span>

1. <span data-ttu-id="68dac-258">In the **User** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-258">In the **User** window, do the following:</span></span>

    ![The User window](./media/paloaltoadmin-tutorial/create_aaduser_04.png)

    <span data-ttu-id="68dac-260">a.</span><span class="sxs-lookup"><span data-stu-id="68dac-260">a.</span></span> <span data-ttu-id="68dac-261">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68dac-261">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68dac-262">b.</span><span class="sxs-lookup"><span data-stu-id="68dac-262">b.</span></span> <span data-ttu-id="68dac-263">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68dac-263">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="68dac-264">c.</span><span class="sxs-lookup"><span data-stu-id="68dac-264">c.</span></span> <span data-ttu-id="68dac-265">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="68dac-265">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="68dac-266">d.</span><span class="sxs-lookup"><span data-stu-id="68dac-266">d.</span></span> <span data-ttu-id="68dac-267">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="68dac-267">Select **Create**.</span></span>
 
### <a name="create-a-palo-alto-networks---admin-ui-test-user"></a><span data-ttu-id="68dac-268">Create a Palo Alto Networks - Admin UI test user</span><span class="sxs-lookup"><span data-stu-id="68dac-268">Create a Palo Alto Networks - Admin UI test user</span></span>

<span data-ttu-id="68dac-269">Palo Alto Networks - Admin UI supports just-in-time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="68dac-269">Palo Alto Networks - Admin UI supports just-in-time user provisioning.</span></span> <span data-ttu-id="68dac-270">If a user doesn't already exist, it is automatically created in the system after a successful authentication.</span><span class="sxs-lookup"><span data-stu-id="68dac-270">If a user doesn't already exist, it is automatically created in the system after a successful authentication.</span></span> <span data-ttu-id="68dac-271">No action is required from you to create the user.</span><span class="sxs-lookup"><span data-stu-id="68dac-271">No action is required from you to create the user.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="68dac-272">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="68dac-272">Assign the Azure AD test user</span></span>

<span data-ttu-id="68dac-273">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Admin UI.</span><span class="sxs-lookup"><span data-stu-id="68dac-273">In this section, you enable user Britta Simon to use Azure single sign-on by granting access to Palo Alto Networks - Admin UI.</span></span> <span data-ttu-id="68dac-274">To do so, do the following:</span><span class="sxs-lookup"><span data-stu-id="68dac-274">To do so, do the following:</span></span>

![Assign the user role][200] 

1. <span data-ttu-id="68dac-276">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="68dac-276">In the Azure portal, open the **Applications** view, go to the **Directory** view, and then select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" and "All applications" links][201] 

1. <span data-ttu-id="68dac-278">In the **Applications** list, select **Palo Alto Networks - Admin UI**.</span><span class="sxs-lookup"><span data-stu-id="68dac-278">In the **Applications** list, select **Palo Alto Networks - Admin UI**.</span></span>

    ![The Palo Alto Networks - Admin UI link](./media/paloaltoadmin-tutorial/tutorial_paloaltoadmin_app.png)  

1. <span data-ttu-id="68dac-280">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="68dac-280">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="68dac-282">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="68dac-282">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="68dac-284">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="68dac-284">In the **Users and groups** window, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="68dac-285">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="68dac-285">Select the **Select** button.</span></span>

1. <span data-ttu-id="68dac-286">In the **Add Assignment** window, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="68dac-286">In the **Add Assignment** window, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="68dac-287">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="68dac-287">Test single sign-on</span></span>

<span data-ttu-id="68dac-288">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="68dac-288">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="68dac-289">When you select the Palo Alto Networks - Admin UI tile in the Access Panel, you should be signed in automatically to your Palo Alto Networks - Admin UI application.</span><span class="sxs-lookup"><span data-stu-id="68dac-289">When you select the Palo Alto Networks - Admin UI tile in the Access Panel, you should be signed in automatically to your Palo Alto Networks - Admin UI application.</span></span>

<span data-ttu-id="68dac-290">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68dac-290">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="68dac-291">Additional resources</span><span class="sxs-lookup"><span data-stu-id="68dac-291">Additional resources</span></span>

* [<span data-ttu-id="68dac-292">List of tutorials about integrating SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68dac-292">List of tutorials about integrating SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="68dac-293">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68dac-293">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/paloaltoadmin-tutorial/tutorial_general_01.png
[2]: ./media/paloaltoadmin-tutorial/tutorial_general_02.png
[3]: ./media/paloaltoadmin-tutorial/tutorial_general_03.png
[4]: ./media/paloaltoadmin-tutorial/tutorial_general_04.png

[100]: ./media/paloaltoadmin-tutorial/tutorial_general_100.png

[200]: ./media/paloaltoadmin-tutorial/tutorial_general_200.png
[201]: ./media/paloaltoadmin-tutorial/tutorial_general_201.png
[202]: ./media/paloaltoadmin-tutorial/tutorial_general_202.png
[203]: ./media/paloaltoadmin-tutorial/tutorial_general_203.png

