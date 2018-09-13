---
title: Configure SSL offload - Azure Application Gateway - Azure Portal | Microsoft Docs
description: This page provides instructions to create an application gateway with SSL offload by using the portal
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 0aa7fbf6d08eb1f478fbbdfa20904209aa7e7051
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549281"
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a>Configure an application gateway for SSL offload by using the portal

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)

Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm. SSL offload also simplifies the front-end server setup and management of the web application.

## <a name="scenario"></a>Scenario

The following scenario goes through configuring SSL offload on an existing application gateway. The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Before you begin

To configure SSL offload with an application gateway, a certificate is required. This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL. The certificate needs to be in Personal Information Exchange (pfx) format. This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.

## <a name="add-an-https-listener"></a>Add an HTTPS listener

The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.

### <a name="step-1"></a>Step 1

Navigate to the Azure portal and select an existing application gateway

### <a name="step-2"></a>Step 2

Click Listeners and click the Add button to add a listener.

![app gateway overview blade][1]

### <a name="step-3"></a>Step 3

Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.

**Name** - This value is a friendly name of the listener.

**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.

**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.

**Protocol** - A switch to determine if https or http is used for the front end.

**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.

![add listener blade][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a>Create a rule and associate it to the listener

The listener has now been created. It is time to create a rule to handle the traffic from the listener. Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie based session affinity is used, protocol, port and health probes.

### <a name="step-1"></a>Step 1

Click the **Rules** of the application gateway, and then click Add.

![app gateway rules blade][3]

### <a name="step-2"></a>Step 2

On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step. Choose the appropriate backend pool and http setting and click **OK**

![https settings window][4]

The settings are now saved to the application gateway. The save process for these settings may take a while before they are available to view through the portal or through PowerShell. Once saved the application gateway handles the encryption and decryption of traffic. All traffic between the application gateway and the backend web servers will be handled over http. Any communication back to the client if initiated over https will be returned to the client encrypted.

## <a name="next-steps"></a>Next steps

To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-ssl-portal/figure4.png




