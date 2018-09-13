---
title: Azure AD App Proxy - get started install connector| Microsoft Docs
description: Turn on Application Proxy in the Azure  portal, and install the Connectors for the reverse proxy.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/26/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5227f756e807a30573733bd408144d869caac9ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870249"
---
# <a name="get-started-with-application-proxy-and-install-the-connector"></a><span data-ttu-id="68a63-103">Get started with Application Proxy and install the connector</span><span class="sxs-lookup"><span data-stu-id="68a63-103">Get started with Application Proxy and install the connector</span></span>
<span data-ttu-id="68a63-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68a63-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="68a63-105">If you're not yet aware of the security and productivity benefits Application Proxy brings to your organization, learn more about [How to provide secure remote access to on-premises applications](application-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="68a63-105">If you're not yet aware of the security and productivity benefits Application Proxy brings to your organization, learn more about [How to provide secure remote access to on-premises applications](application-proxy.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="68a63-106">Application Proxy prerequisites</span><span class="sxs-lookup"><span data-stu-id="68a63-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="68a63-107">Before you can enable and use Application Proxy services, you need to have:</span><span class="sxs-lookup"><span data-stu-id="68a63-107">Before you can enable and use Application Proxy services, you need to have:</span></span>

* <span data-ttu-id="68a63-108">A [Microsoft Azure AD basic or premium subscription](../fundamentals/active-directory-whatis.md) and an Azure AD directory for which you are a global administrator.</span><span class="sxs-lookup"><span data-stu-id="68a63-108">A [Microsoft Azure AD basic or premium subscription](../fundamentals/active-directory-whatis.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="68a63-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span><span class="sxs-lookup"><span data-stu-id="68a63-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span></span> <span data-ttu-id="68a63-110">The server needs to be able to connect to the Application Proxy services in the cloud, and the on-premises applications that you are publishing.</span><span class="sxs-lookup"><span data-stu-id="68a63-110">The server needs to be able to connect to the Application Proxy services in the cloud, and the on-premises applications that you are publishing.</span></span>
  * <span data-ttu-id="68a63-111">For single sign-on to your published applications using Kerberos Constrained Delegation, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span><span class="sxs-lookup"><span data-stu-id="68a63-111">For single sign-on to your published applications using Kerberos Constrained Delegation, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span></span> <span data-ttu-id="68a63-112">For information, see [KCD for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="68a63-112">For information, see [KCD for single sign-on with Application Proxy](application-proxy-configure-single-sign-on-with-kcd.md).</span></span>

<span data-ttu-id="68a63-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers.md) for details on how to configure them before you get started with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="68a63-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers.md) for details on how to configure them before you get started with Application Proxy.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="68a63-114">Open your ports</span><span class="sxs-lookup"><span data-stu-id="68a63-114">Open your ports</span></span>

<span data-ttu-id="68a63-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="68a63-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span></span> <span data-ttu-id="68a63-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="68a63-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span></span>

1. <span data-ttu-id="68a63-117">Open the following ports to **outbound** traffic:</span><span class="sxs-lookup"><span data-stu-id="68a63-117">Open the following ports to **outbound** traffic:</span></span>

   | <span data-ttu-id="68a63-118">Port number</span><span class="sxs-lookup"><span data-stu-id="68a63-118">Port number</span></span> | <span data-ttu-id="68a63-119">How it's used</span><span class="sxs-lookup"><span data-stu-id="68a63-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="68a63-120">80</span><span class="sxs-lookup"><span data-stu-id="68a63-120">80</span></span> | <span data-ttu-id="68a63-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="68a63-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="68a63-122">443</span><span class="sxs-lookup"><span data-stu-id="68a63-122">443</span></span> | <span data-ttu-id="68a63-123">All outbound communication with the Application Proxy service</span><span class="sxs-lookup"><span data-stu-id="68a63-123">All outbound communication with the Application Proxy service</span></span> |

   <span data-ttu-id="68a63-124">If your firewall enforces traffic according to originating users, open these ports for traffic from Windows services that run as a Network Service.</span><span class="sxs-lookup"><span data-stu-id="68a63-124">If your firewall enforces traffic according to originating users, open these ports for traffic from Windows services that run as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="68a63-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span><span class="sxs-lookup"><span data-stu-id="68a63-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="68a63-126">If you still have an older connector version, you also need to enable the following ports in addition to 80 and 443: 5671, 8080, 9090-9091, 9350, 9352, 10100–10120.</span><span class="sxs-lookup"><span data-stu-id="68a63-126">If you still have an older connector version, you also need to enable the following ports in addition to 80 and 443: 5671, 8080, 9090-9091, 9350, 9352, 10100–10120.</span></span>
   >
   ><span data-ttu-id="68a63-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md#automatic-updates).</span><span class="sxs-lookup"><span data-stu-id="68a63-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="68a63-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span><span class="sxs-lookup"><span data-stu-id="68a63-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="68a63-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span><span class="sxs-lookup"><span data-stu-id="68a63-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="68a63-130">Microsoft uses four addresses to verify certificates.</span><span class="sxs-lookup"><span data-stu-id="68a63-130">Microsoft uses four addresses to verify certificates.</span></span> <span data-ttu-id="68a63-131">Allow access to the following URLs if you haven't done so for other products:</span><span class="sxs-lookup"><span data-stu-id="68a63-131">Allow access to the following URLs if you haven't done so for other products:</span></span>
   * <span data-ttu-id="68a63-132">mscrl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="68a63-132">mscrl.microsoft.com:80</span></span>
   * <span data-ttu-id="68a63-133">crl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="68a63-133">crl.microsoft.com:80</span></span>
   * <span data-ttu-id="68a63-134">ocsp.msocsp.com:80</span><span class="sxs-lookup"><span data-stu-id="68a63-134">ocsp.msocsp.com:80</span></span>
   * <span data-ttu-id="68a63-135">www.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="68a63-135">www.microsoft.com:80</span></span>

4. <span data-ttu-id="68a63-136">Your connector needs access to login.windows.net and login.microsoftonline.com for the registration process.</span><span class="sxs-lookup"><span data-stu-id="68a63-136">Your connector needs access to login.windows.net and login.microsoftonline.com for the registration process.</span></span>


## <a name="install-and-register-a-connector"></a><span data-ttu-id="68a63-137">Install and register a connector</span><span class="sxs-lookup"><span data-stu-id="68a63-137">Install and register a connector</span></span>
1. <span data-ttu-id="68a63-138">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68a63-138">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68a63-139">Your current directory appears under your username in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="68a63-139">Your current directory appears under your username in the top right corner.</span></span> <span data-ttu-id="68a63-140">If you need to change directories, select that icon.</span><span class="sxs-lookup"><span data-stu-id="68a63-140">If you need to change directories, select that icon.</span></span>
3. <span data-ttu-id="68a63-141">Go to **Azure Active Directory** > **Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="68a63-141">Go to **Azure Active Directory** > **Application Proxy**.</span></span>

   ![Navigate to Application Proxy](./media/application-proxy-enable/app_proxy_navigate.png)

4. <span data-ttu-id="68a63-143">Select **Download Connector**.</span><span class="sxs-lookup"><span data-stu-id="68a63-143">Select **Download Connector**.</span></span>

   ![Download Connector](./media/application-proxy-enable/download_connector.png)

5. <span data-ttu-id="68a63-145">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="68a63-145">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span></span>
6. <span data-ttu-id="68a63-146">Follow the instructions in the wizard to install.</span><span class="sxs-lookup"><span data-stu-id="68a63-146">Follow the instructions in the wizard to install.</span></span> <span data-ttu-id="68a63-147">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="68a63-147">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="68a63-148">Provide your Azure AD global administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="68a63-148">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="68a63-149">Your global administrator tenant may be different from your Microsoft Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="68a63-149">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="68a63-150">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span><span class="sxs-lookup"><span data-stu-id="68a63-150">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="68a63-151">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span><span class="sxs-lookup"><span data-stu-id="68a63-151">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="68a63-152">If **IE Enhanced Security Configuration** is set to **On** on the server where you are installing the connector, you may not see the registration screen.</span><span class="sxs-lookup"><span data-stu-id="68a63-152">If **IE Enhanced Security Configuration** is set to **On** on the server where you are installing the connector, you may not see the registration screen.</span></span> <span data-ttu-id="68a63-153">To get access, follow the instructions in the error message.</span><span class="sxs-lookup"><span data-stu-id="68a63-153">To get access, follow the instructions in the error message.</span></span> <span data-ttu-id="68a63-154">Make sure that Internet Explorer Enhanced Security is off.</span><span class="sxs-lookup"><span data-stu-id="68a63-154">Make sure that Internet Explorer Enhanced Security is off.</span></span>

<span data-ttu-id="68a63-155">For high availability purposes, you should deploy at least two connectors.</span><span class="sxs-lookup"><span data-stu-id="68a63-155">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="68a63-156">Each connector must be registered separately.</span><span class="sxs-lookup"><span data-stu-id="68a63-156">Each connector must be registered separately.</span></span>

## <a name="test-that-the-connector-installed-correctly"></a><span data-ttu-id="68a63-157">Test that the connector installed correctly</span><span class="sxs-lookup"><span data-stu-id="68a63-157">Test that the connector installed correctly</span></span>

<span data-ttu-id="68a63-158">You can confirm that a new connector installed correctly by checking for it in either the Azure portal or on your server.</span><span class="sxs-lookup"><span data-stu-id="68a63-158">You can confirm that a new connector installed correctly by checking for it in either the Azure portal or on your server.</span></span> 

<span data-ttu-id="68a63-159">In the Azure portal, sign in to your tenant and navigate to **Azure Active Directory** > **Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="68a63-159">In the Azure portal, sign in to your tenant and navigate to **Azure Active Directory** > **Application Proxy**.</span></span> <span data-ttu-id="68a63-160">All of your connectors and connector groups appear on this page.</span><span class="sxs-lookup"><span data-stu-id="68a63-160">All of your connectors and connector groups appear on this page.</span></span> <span data-ttu-id="68a63-161">Select a connector to see its details or move it into a different connector group.</span><span class="sxs-lookup"><span data-stu-id="68a63-161">Select a connector to see its details or move it into a different connector group.</span></span> 

<span data-ttu-id="68a63-162">On your server, check the list of active services for the connector and the connector updater.</span><span class="sxs-lookup"><span data-stu-id="68a63-162">On your server, check the list of active services for the connector and the connector updater.</span></span> <span data-ttu-id="68a63-163">The two services should start running immediately, but if not, turn them on:</span><span class="sxs-lookup"><span data-stu-id="68a63-163">The two services should start running immediately, but if not, turn them on:</span></span> 

   * <span data-ttu-id="68a63-164">**Microsoft AAD Application Proxy Connector** enables connectivity</span><span class="sxs-lookup"><span data-stu-id="68a63-164">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

   * <span data-ttu-id="68a63-165">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span><span class="sxs-lookup"><span data-stu-id="68a63-165">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="68a63-166">The updater checks for new versions of the connector and updates the connector as needed.</span><span class="sxs-lookup"><span data-stu-id="68a63-166">The updater checks for new versions of the connector and updates the connector as needed.</span></span>

   ![App Proxy Connector services - screenshot](./media/application-proxy-enable/app_proxy_services.png)

<span data-ttu-id="68a63-168">For information about connectors and how they stay up to date, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="68a63-168">For information about connectors and how they stay up to date, see [Understand Azure AD Application Proxy connectors](application-proxy-connectors.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="68a63-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="68a63-169">Next steps</span></span>
<span data-ttu-id="68a63-170">You are now ready to [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68a63-170">You are now ready to [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="68a63-171">If you have applications that are on separate networks or different locations, use connector groups to organize the different connectors into logical units.</span><span class="sxs-lookup"><span data-stu-id="68a63-171">If you have applications that are on separate networks or different locations, use connector groups to organize the different connectors into logical units.</span></span> <span data-ttu-id="68a63-172">Learn more about [Working with Application Proxy connectors](application-proxy-connector-groups.md).</span><span class="sxs-lookup"><span data-stu-id="68a63-172">Learn more about [Working with Application Proxy connectors](application-proxy-connector-groups.md).</span></span>
