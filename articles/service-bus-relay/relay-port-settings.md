---
title: Azure Relay port settings | Microsoft Docs
description: Details about Azure Relay port values.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: sethm
ms.openlocfilehash: 783e797ad318fe926ba9e72e2eea027beb4a5994
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563874"
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="461aa-103">Azure Relay port settings</span><span class="sxs-lookup"><span data-stu-id="461aa-103">Azure Relay port settings</span></span>

<span data-ttu-id="461aa-104">The following table describes the required configuration for port values for a Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="461aa-104">The following table describes the required configuration for port values for a Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="461aa-105">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="461aa-105">Hybrid Connections</span></span>
<span data-ttu-id="461aa-106">Hybrid Connections uses WebSockets as the underlying transport mechanism, which uses **HTTPS** only.</span><span class="sxs-lookup"><span data-stu-id="461aa-106">Hybrid Connections uses WebSockets as the underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="461aa-107">WCF Relays</span><span class="sxs-lookup"><span data-stu-id="461aa-107">WCF Relays</span></span>
  
|<span data-ttu-id="461aa-108">Binding</span><span class="sxs-lookup"><span data-stu-id="461aa-108">Binding</span></span>|<span data-ttu-id="461aa-109">Transport Security</span><span class="sxs-lookup"><span data-stu-id="461aa-109">Transport Security</span></span>|<span data-ttu-id="461aa-110">Port</span><span class="sxs-lookup"><span data-stu-id="461aa-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="461aa-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="461aa-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="461aa-112">Yes</span><span class="sxs-lookup"><span data-stu-id="461aa-112">Yes</span></span>|<span data-ttu-id="461aa-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="461aa-113">HTTPS</span></span>| 
| |<span data-ttu-id="461aa-114">"</span><span class="sxs-lookup"><span data-stu-id="461aa-114">"</span></span> |<span data-ttu-id="461aa-115">No</span><span class="sxs-lookup"><span data-stu-id="461aa-115">No</span></span>|<span data-ttu-id="461aa-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-116">HTTP</span></span>|  
|<span data-ttu-id="461aa-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="461aa-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="461aa-118">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-118">Either</span></span>|<span data-ttu-id="461aa-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-119">9351/HTTP</span></span>|  
|<span data-ttu-id="461aa-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="461aa-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="461aa-121">Yes</span><span class="sxs-lookup"><span data-stu-id="461aa-121">Yes</span></span>|<span data-ttu-id="461aa-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="461aa-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="461aa-123">"</span><span class="sxs-lookup"><span data-stu-id="461aa-123">"</span></span> |<span data-ttu-id="461aa-124">No</span><span class="sxs-lookup"><span data-stu-id="461aa-124">No</span></span>|<span data-ttu-id="461aa-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-125">9350/HTTP</span></span>|  
|<span data-ttu-id="461aa-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="461aa-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="461aa-127">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-127">Either</span></span>|<span data-ttu-id="461aa-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-128">9351/HTTP</span></span>|  
|<span data-ttu-id="461aa-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span><span class="sxs-lookup"><span data-stu-id="461aa-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="461aa-130">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-130">Either</span></span>|<span data-ttu-id="461aa-131">5671/9352/HTTP (9352/9353 if using hybrid)</span><span class="sxs-lookup"><span data-stu-id="461aa-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="461aa-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="461aa-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="461aa-133">Yes</span><span class="sxs-lookup"><span data-stu-id="461aa-133">Yes</span></span>|<span data-ttu-id="461aa-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="461aa-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="461aa-135">"</span><span class="sxs-lookup"><span data-stu-id="461aa-135">"</span></span> |<span data-ttu-id="461aa-136">No</span><span class="sxs-lookup"><span data-stu-id="461aa-136">No</span></span>|<span data-ttu-id="461aa-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-137">9350/HTTP</span></span>|  
|<span data-ttu-id="461aa-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="461aa-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="461aa-139">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-139">Either</span></span>|<span data-ttu-id="461aa-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-140">9351/HTTP</span></span>|  
|<span data-ttu-id="461aa-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="461aa-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="461aa-142">Yes</span><span class="sxs-lookup"><span data-stu-id="461aa-142">Yes</span></span>|<span data-ttu-id="461aa-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="461aa-143">HTTPS</span></span>|  
||<span data-ttu-id="461aa-144">"</span><span class="sxs-lookup"><span data-stu-id="461aa-144">"</span></span> |<span data-ttu-id="461aa-145">No</span><span class="sxs-lookup"><span data-stu-id="461aa-145">No</span></span>|<span data-ttu-id="461aa-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-146">HTTP</span></span>|  
|<span data-ttu-id="461aa-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="461aa-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="461aa-148">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-148">Either</span></span>|<span data-ttu-id="461aa-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-149">9351/HTTP</span></span>|  
|<span data-ttu-id="461aa-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span><span class="sxs-lookup"><span data-stu-id="461aa-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="461aa-151">Yes</span><span class="sxs-lookup"><span data-stu-id="461aa-151">Yes</span></span>|<span data-ttu-id="461aa-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="461aa-152">HTTPS</span></span>|  
||<span data-ttu-id="461aa-153">"</span><span class="sxs-lookup"><span data-stu-id="461aa-153">"</span></span> |<span data-ttu-id="461aa-154">No</span><span class="sxs-lookup"><span data-stu-id="461aa-154">No</span></span>|<span data-ttu-id="461aa-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-155">HTTP</span></span>|  
|<span data-ttu-id="461aa-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span><span class="sxs-lookup"><span data-stu-id="461aa-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="461aa-157">Either</span><span class="sxs-lookup"><span data-stu-id="461aa-157">Either</span></span>|<span data-ttu-id="461aa-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="461aa-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="461aa-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="461aa-159">Next steps</span></span>
<span data-ttu-id="461aa-160">To learn more about Azure Relay, visit these links:</span><span class="sxs-lookup"><span data-stu-id="461aa-160">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="461aa-161">What is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="461aa-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="461aa-162">Relay FAQ</span><span class="sxs-lookup"><span data-stu-id="461aa-162">Relay FAQ</span></span>](relay-faq.md)