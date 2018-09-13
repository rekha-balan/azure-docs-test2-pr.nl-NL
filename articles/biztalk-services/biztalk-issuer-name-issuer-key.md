---
title: Issuer Name and Issuer Key in BizTalk Services | Microsoft Docs
description: Learn how to retrieve Issuer Name and Issuer Key for either Service Bus or Access Control (ACS) in BizTalk Services. MABS, WABS
services: biztalk-services
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4fb13a158c660105a5fc8f79a92c67ba65c5356d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669631"
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk Services: Issuer Name and Issuer Key
Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key. Specifically:

| Task | Which Issuer Name and Issuer Key |
| --- | --- |
| Deploying your application from Visual Studio |Access Control Issuer Name and Issuer Key |
| Configuring the Azure BizTalk Services Portal |Access Control Issuer Name and Issuer Key |
| Creating LOB Relays with the BizTalk Adapter Services in Visual Studio |Service Bus Issuer Name and Issuer Key |

This topic lists the steps to retrieve the Issuer Name and Issuer Key. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Access Control Issuer Name and Issuer Key
The Access Control Issuer Name and Issuer Key are used by the following:

* Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key. 
* The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a>Get the Access Control Issuer Name and Issuer Key

To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:

1. Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Add your Azure account: `Add-AzureAccount`
3. Return your subscription name: `get-azuresubscription`
4. Select your subscription: `select-azuresubscription <name of your subscription>` 
5. Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

To summarize:  
Issuer Name = SharedSecretIssuer  
Issuer Key = SharedSecretKey

More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Service Bus Issuer Name and Issuer Key
Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services. In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system. To connect, you create the LOB Relay and enter your LOB system details. When doing this, you also enter the Service Bus Issuer Name and Issuer Key.

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a>To retrieve the Service Bus Issuer Name and Issuer Key
1. Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. In the left navigation pane, select **Service Bus**.
3. Select your namespace. In the task bar, select **Connection Information**. This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key). Their values can be copied.  

To summarize:  
Issuer Name = Default Issuer  
Issuer Key = Default Key

## <a name="next"></a>Next
Additional Azure BizTalk Services topics:

* [Installing the Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutorials: Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [How do I Start Using the Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>See Also
* [How to: Use ACS Management Service to Configure Service Identities](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [BizTalk Services: Developer, Basic, Standard and Premium Editions Chart](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: Provisioning Status Chart](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: Dashboard, Monitor and Scale tabs](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: Backup and Restore](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: Throttling](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

