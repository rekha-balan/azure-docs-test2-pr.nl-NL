---
title: Create an application gateway using the portal | Microsoft Docs
description: Learn how to create an Application Gateway by using the portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: gwallace
ms.openlocfilehash: f8657a4cff8ee937cd749223cc3ebb28871512ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555219"
---
# <a name="create-an-application-gateway-by-using-the-portal"></a>Create an application gateway by using the portal

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway is a layer-7 load balancer. It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.
Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.

To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)

## <a name="scenario"></a>Scenario

In this scenario, you learn how to create an application gateway using the Azure portal.

This scenario will:

* Create a medium application gateway with two instances.
* Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.
* Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.
* Configure a certificate for SSL offload.

![Scenario example][scenario]

> [!IMPORTANT]
> Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.

## <a name="before-you-begin"></a>Before you begin

Azure Application Gateway requires its own subnet. When creating a virtual network, ensure that you leave enough address space to have multiple subnets. Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.

## <a name="create-the-application-gateway"></a>Create the Application Gateway

### <a name="step-1"></a>Step 1

Navigate to the Azure portal, click **New** > **Networking** > **Application Gateway**

![Creating Application Gateway][1]

### <a name="step-2"></a>Step 2

Next fill out the basic information about the application gateway. When complete click **OK**

The information needed for the basic settings is:

* **Name** - The name for the application gateway.
* **Tier** - This setting is the tier of the application gateway. Two tiers are available, **WAF** and **Standard**. WAF enables the web application firewall feature.
* **SKU size** - This setting is the size of the application gateway, available options are ( **Small**, **Medium**, and **Large** ). Small is not available when WAF tier is chosen.
* **Instance count** - The number of instances, this value should be a number between 2 and 10.
* **Resource group** - The resource group to hold the application gateway, it can be an existing resource group or a new one.
* **Location** - The region for the application gateway, it is the same location at the resource group. The location is important as the virtual network and public IP must be in the same location as the gateway.

![blade showing basic settings][2]

> [!NOTE]
> An instance count of 1 can be chosen for testing purposes. It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended. Small gateways are to be used for dev test and not for production purposes.
> 
> 

### <a name="step-3"></a>Step 3

Once the basic settings are defined, the next step is to define the virtual network to be used. The virtual network houses the application that the application gateway does load balancing for.

Click **Choose a virtual network** to configure the virtual network.

![blade showing settings for application gateway][3]

### <a name="step-4"></a>Step 4

In the **Choose Virtual Network** blade, click **Create New**

While not explained in this scenario, an existing Virtual Network could be selected at this point.  If an existing virtual network is used, it is important to know that the virtual network needs an empty subnet or a subnet of only application gateway resources to be used.

![choose virtual network blade][4]

### <a name="step-5"></a>Step 5

Fill out the network information in the **Create Virtual Network** blade as described in the preceding [Scenario](#scenario) description.

![Create virtual network blade with information entered][5]

### <a name="step-6"></a>Step 6

Once the virtual network is created, the next step is to define the front-end IP for the application gateway. At this point, the choice is between a public or a private IP address for the front-end. The choice depends on whether the application is internet facing or internal only. This scenario assumes using a public IP address. To choose a private IP address, the **Private** button can be clicked. An automatically assigned IP address is chosen or you can click the **Choose a specific private IP address** checkbox to enter one manually.

### <a name="step-7"></a>Step 7

Click **Choose a public IP address**. If an existing public IP address is available it can be chosen at this point, in this scenario you create a new public IP address. Click **Create new**

![Choose public IP address blade][6]

### <a name="step-8"></a>Step 8

Next give the public IP address a friendly name and click **OK**

![Create public IP Address blade][7]

### <a name="step-9"></a>Step 9

The last setting to configure when creating an application gateway is the listener configuration.  If **http** is used, nothing is left to configure and **OK** can be clicked. To use **https** further configuration is required.

To use **https**, a certificate is required. The private key of the certificate is needed, a .pfx export of the certificate and password need to be provided.

### <a name="step-10"></a>Step 10

Click **HTTPS**, click the **folder** icon next to the **Upload PFX certificate** textbox.
Navigate to the .pfx certificate file on your file system. Once it is selected, give the certificate a friendly name and type the password for the .pfx file.

Once complete click **OK** to review the settings for the Application Gateway.

![Listener Configuration section on Settings blade][9]

### <a name="step-11"></a>Step 11

Review the Summary page and click **OK**.  Now the application gateway is queued up and created.

### <a name="step-12"></a>Step 12

Once the application gateway has been created, navigate to it in the portal to continue configuration of the application gateway.

![Application Gateway resource view][10]

These steps create a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules. You can modify these settings to suit your deployment once the provisioning is successful.

## <a name="add-servers-to-backend-pools"></a>Add servers to backend pools

Once the application gateway is created, the systems that host the application to be load balanced still need to be added to the application gateway. The IP addresses or FQDN values of these servers are added to the backend address pools.

### <a name="ip-address-or-fqdn"></a>IP Address or FQDN

#### <a name="step-1"></a>Step 1

Click the application gateway you created, click **Backend pools**, and select the current backend pool.

![Application Gateway backend pools][11]

#### <a name="step-2"></a>Step 2

Click **Add Target** to add IP addresses of FQDN values

![Application Gateway backend pools][11-1]

#### <a name="step-3"></a>Step 3

Once all backend values are entered, click **Save**

![add values to application gateway backend pools][12]

This action saves the values in the backend pool. Once the application gateway has been updated, traffic that enters the application gateway is routed to the backend addresses added in this step.

### <a name="virtual-machine-and-nic"></a>Virtual Machine and NIC

You can also add Virtual Machine NICs as backend pool members. Only virtual machines within the same virtual network as the Application Gateway are available through the dropdown.

#### <a name="step-1"></a>Step 1

Click the application gateway you created, click **Backend pools**, and select the current backend pool.

![Application Gateway backend pools][11]

#### <a name="step-2"></a>Step 2

Click **Add Target** to add a new backend pool member. Choose a virtual machine and a NIC from the dropdown boxes.

![add nics to application gateway backend pools][13]

#### <a name="step-3"></a>Step 3

When complete, click **Save** to save the NICs as backend members.

![save nic application gateway backend pools][14]

## <a name="next-steps"></a>Next steps

This scenario creates a default application gateway. The next steps are to configure the application gateway by modifying settings, and adjusting rules in the gateway. These steps can be found by visiting the following articles:

Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)

Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)

Learn how to protect your applications with [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) a feature of application gateway.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure11.png
[11-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure11-1.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/figure14.png
[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-portal/scenario.png
















