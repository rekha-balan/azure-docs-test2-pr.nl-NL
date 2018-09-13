---
title: Azure Relay port settings | Microsoft Docs
description: Details about Azure Relay port values.
services: service-bus-relay
documentationcenter: na
author: spelluru
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2018
ms.author: spelluru
ms.openlocfilehash: 3ef08cfc94a029f97250578e9b0366a18770c809
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825175"
---
# <a name="azure-relay-port-settings"></a>Azure Relay port settings

The following table describes the required configuration for port values for Azure Relay.

## <a name="hybrid-connections"></a>Hybrid Connections

Hybrid Connections uses WebSockets on port 443 with SSL as the underlying transport mechanism, which uses **HTTPS** only. 

## <a name="wcf-relays"></a>WCF Relays
  
|Binding|Transport Security|Port|  
|-------------|------------------------|----------|  
|[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)|Yes|HTTPS| 
|" |No|HTTP|  
|[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)|Either|9351/HTTP|  
|[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)|Yes|9351/HTTPS|  
|" |No|9350/HTTP|  
|[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)|Either|9351/HTTP|  
|[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)|Either|5671/9352/HTTP (9352/9353 if using hybrid)|  
|[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)|Yes|9351/HTTPS|  
|" |No|9350/HTTP|  
|[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)|Either|9351/HTTP|  
|[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)|Yes|HTTPS|  
|" |No|HTTP|  
|[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)|Either|9351/HTTP|  
|[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)|Yes|HTTPS|  
|" |No|HTTP|  
|[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)|Either|9351/HTTP|

## <a name="next-steps"></a>Next steps
To learn more about Azure Relay, visit these links:
* [What is Azure Relay?](relay-what-is-it.md)
* [Relay FAQ](relay-faq.md)