---
title: Problem installing the Application Proxy Agent Connector | Microsoft Docs
description: How to troubleshoot issues you might face when installing the Application Proxy Agent Connector
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: a7d62520bb95198f5b11f6e6414031799dc7cd07
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549774"
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a>Problem installing the Application Proxy Agent Connector

Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.

## <a name="general-problem-areas-with-connector-installation"></a>General Problem Areas with Connector installation

When the installation of a connector fails, the root cause is usually one of the following areas:

1.  **Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties. This is done by connecting to the AAD Application Proxy cloud service.

2.  **Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.

3.  **Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a>Verify connectivity to the Cloud Application Proxy service and Microsoft Login page

**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.

1.  Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.

2.  If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.

3.  Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Verify Machine and backend components support for Application Proxy trust cert

**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.

>[!NOTE]
>The connector tries to create a SHA512 cert that is supported by TLS1.2. If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.
>
>

**To resolve the issue:**

1.  Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2. If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.

## <a name="verify-admin-is-used-to-install-the-connector"></a>Verify admin is used to install the connector

**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials. Currently, the user must be a global administrator for the installation to succeed.

**To verify the credentials are correct:**

Connect to <https://login.microsoftonline.com> and use the same credentials. Make sure the login is successful. You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**. 

Select your user account, then “Directory Role” in the resulting menu. Verify that the selected role is “Global administrator”. If you are unable to access any of the pages along these steps, you are not a global administrator.

## <a name="next-steps"></a>Next steps
[Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md)
