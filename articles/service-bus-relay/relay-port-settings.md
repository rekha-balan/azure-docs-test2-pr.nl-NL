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
# <a name="azure-relay-port-settings"></a><span data-ttu-id="f996a-103">Azure Relay port settings</span><span class="sxs-lookup"><span data-stu-id="f996a-103">Azure Relay port settings</span></span>

<span data-ttu-id="f996a-104">The following table describes the required configuration for port values for Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="f996a-104">The following table describes the required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="f996a-105">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="f996a-105">Hybrid Connections</span></span>

<span data-ttu-id="f996a-106">Hybrid Connections uses WebSockets on port 443 with SSL as the underlying transport mechanism, which uses **HTTPS** only.</span><span class="sxs-lookup"><span data-stu-id="f996a-106">Hybrid Connections uses WebSockets on port 443 with SSL as the underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="f996a-107">WCF Relays</span><span class="sxs-lookup"><span data-stu-id="f996a-107">WCF Relays</span></span>
  
|<span data-ttu-id="f996a-108">Binding</span><span class="sxs-lookup"><span data-stu-id="f996a-108">Binding</span></span>|<span data-ttu-id="f996a-109">Transport Security</span><span class="sxs-lookup"><span data-stu-id="f996a-109">Transport Security</span></span>|<span data-ttu-id="f996a-110">Port</span><span class="sxs-lookup"><span data-stu-id="f996a-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="f996a-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="f996a-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="f996a-112">Yes</span><span class="sxs-lookup"><span data-stu-id="f996a-112">Yes</span></span>|<span data-ttu-id="f996a-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f996a-113">HTTPS</span></span>| 
|<span data-ttu-id="f996a-114">"</span><span class="sxs-lookup"><span data-stu-id="f996a-114">"</span></span> |<span data-ttu-id="f996a-115">No</span><span class="sxs-lookup"><span data-stu-id="f996a-115">No</span></span>|<span data-ttu-id="f996a-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-116">HTTP</span></span>|  
|<span data-ttu-id="f996a-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="f996a-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="f996a-118">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-118">Either</span></span>|<span data-ttu-id="f996a-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-119">9351/HTTP</span></span>|  
|<span data-ttu-id="f996a-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="f996a-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="f996a-121">Yes</span><span class="sxs-lookup"><span data-stu-id="f996a-121">Yes</span></span>|<span data-ttu-id="f996a-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="f996a-122">9351/HTTPS</span></span>|  
|<span data-ttu-id="f996a-123">"</span><span class="sxs-lookup"><span data-stu-id="f996a-123">"</span></span> |<span data-ttu-id="f996a-124">No</span><span class="sxs-lookup"><span data-stu-id="f996a-124">No</span></span>|<span data-ttu-id="f996a-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-125">9350/HTTP</span></span>|  
|<span data-ttu-id="f996a-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="f996a-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="f996a-127">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-127">Either</span></span>|<span data-ttu-id="f996a-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-128">9351/HTTP</span></span>|  
|<span data-ttu-id="f996a-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span><span class="sxs-lookup"><span data-stu-id="f996a-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="f996a-130">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-130">Either</span></span>|<span data-ttu-id="f996a-131">5671/9352/HTTP (9352/9353 if using hybrid)</span><span class="sxs-lookup"><span data-stu-id="f996a-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="f996a-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="f996a-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="f996a-133">Yes</span><span class="sxs-lookup"><span data-stu-id="f996a-133">Yes</span></span>|<span data-ttu-id="f996a-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="f996a-134">9351/HTTPS</span></span>|  
|<span data-ttu-id="f996a-135">"</span><span class="sxs-lookup"><span data-stu-id="f996a-135">"</span></span> |<span data-ttu-id="f996a-136">No</span><span class="sxs-lookup"><span data-stu-id="f996a-136">No</span></span>|<span data-ttu-id="f996a-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-137">9350/HTTP</span></span>|  
|<span data-ttu-id="f996a-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="f996a-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="f996a-139">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-139">Either</span></span>|<span data-ttu-id="f996a-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-140">9351/HTTP</span></span>|  
|<span data-ttu-id="f996a-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="f996a-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="f996a-142">Yes</span><span class="sxs-lookup"><span data-stu-id="f996a-142">Yes</span></span>|<span data-ttu-id="f996a-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f996a-143">HTTPS</span></span>|  
|<span data-ttu-id="f996a-144">"</span><span class="sxs-lookup"><span data-stu-id="f996a-144">"</span></span> |<span data-ttu-id="f996a-145">No</span><span class="sxs-lookup"><span data-stu-id="f996a-145">No</span></span>|<span data-ttu-id="f996a-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-146">HTTP</span></span>|  
|<span data-ttu-id="f996a-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="f996a-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="f996a-148">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-148">Either</span></span>|<span data-ttu-id="f996a-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-149">9351/HTTP</span></span>|  
|<span data-ttu-id="f996a-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="f996a-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="f996a-151">Yes</span><span class="sxs-lookup"><span data-stu-id="f996a-151">Yes</span></span>|<span data-ttu-id="f996a-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f996a-152">HTTPS</span></span>|  
|<span data-ttu-id="f996a-153">"</span><span class="sxs-lookup"><span data-stu-id="f996a-153">"</span></span> |<span data-ttu-id="f996a-154">No</span><span class="sxs-lookup"><span data-stu-id="f996a-154">No</span></span>|<span data-ttu-id="f996a-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-155">HTTP</span></span>|  
|<span data-ttu-id="f996a-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="f996a-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="f996a-157">Either</span><span class="sxs-lookup"><span data-stu-id="f996a-157">Either</span></span>|<span data-ttu-id="f996a-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="f996a-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f996a-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="f996a-159">Next steps</span></span>
<span data-ttu-id="f996a-160">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="f996a-160">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="f996a-161">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="f996a-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f996a-162">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="f996a-162">Relay FAQ</span></span>](relay-faq.md)