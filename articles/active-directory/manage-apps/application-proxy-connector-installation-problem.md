---
title: Problem installing the Application Proxy Agent Connector | Microsoft Docs
description: How to troubleshoot issues you might face when installing the Application Proxy Agent Connector
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 98dc3981e0f34ebfe7d8881d77b84cfe252e3f4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864419"
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="f66a7-103">Problem installing the Application Proxy Agent Connector</span><span class="sxs-lookup"><span data-stu-id="f66a7-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="f66a7-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span><span class="sxs-lookup"><span data-stu-id="f66a7-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="f66a7-105">General Problem Areas with Connector installation</span><span class="sxs-lookup"><span data-stu-id="f66a7-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="f66a7-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span><span class="sxs-lookup"><span data-stu-id="f66a7-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="f66a7-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span><span class="sxs-lookup"><span data-stu-id="f66a7-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="f66a7-108">This is done by connecting to the AAD Application Proxy cloud service.</span><span class="sxs-lookup"><span data-stu-id="f66a7-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="f66a7-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="f66a7-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="f66a7-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span><span class="sxs-lookup"><span data-stu-id="f66a7-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="f66a7-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span><span class="sxs-lookup"><span data-stu-id="f66a7-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="f66a7-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span><span class="sxs-lookup"><span data-stu-id="f66a7-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="f66a7-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 80 and 443 is working.</span><span class="sxs-lookup"><span data-stu-id="f66a7-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 80 and 443 is working.</span></span>

2.  <span data-ttu-id="f66a7-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 80 and 443 defined correctly.</span><span class="sxs-lookup"><span data-stu-id="f66a7-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 80 and 443 defined correctly.</span></span>

3.  <span data-ttu-id="f66a7-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span><span class="sxs-lookup"><span data-stu-id="f66a7-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="f66a7-116">Verify Machine and backend components support for Application Proxy trust cert</span><span class="sxs-lookup"><span data-stu-id="f66a7-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="f66a7-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span><span class="sxs-lookup"><span data-stu-id="f66a7-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="f66a7-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="f66a7-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="f66a7-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span><span class="sxs-lookup"><span data-stu-id="f66a7-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="f66a7-120">**To resolve the issue:**</span><span class="sxs-lookup"><span data-stu-id="f66a7-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="f66a7-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f66a7-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="f66a7-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="f66a7-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="f66a7-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span><span class="sxs-lookup"><span data-stu-id="f66a7-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="f66a7-124">Verify admin is used to install the connector</span><span class="sxs-lookup"><span data-stu-id="f66a7-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="f66a7-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span><span class="sxs-lookup"><span data-stu-id="f66a7-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="f66a7-126">Currently, the user must be a global administrator for the installation to succeed.</span><span class="sxs-lookup"><span data-stu-id="f66a7-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="f66a7-127">**To verify the credentials are correct:**</span><span class="sxs-lookup"><span data-stu-id="f66a7-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="f66a7-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span><span class="sxs-lookup"><span data-stu-id="f66a7-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="f66a7-129">Make sure the login is successful.</span><span class="sxs-lookup"><span data-stu-id="f66a7-129">Make sure the login is successful.</span></span> <span data-ttu-id="f66a7-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span><span class="sxs-lookup"><span data-stu-id="f66a7-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="f66a7-131">Select your user account, then “Directory Role” in the resulting menu.</span><span class="sxs-lookup"><span data-stu-id="f66a7-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="f66a7-132">Verify that the selected role is “Global administrator”.</span><span class="sxs-lookup"><span data-stu-id="f66a7-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="f66a7-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span><span class="sxs-lookup"><span data-stu-id="f66a7-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66a7-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="f66a7-134">Next steps</span></span>
[<span data-ttu-id="f66a7-135">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="f66a7-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-connectors.md)
