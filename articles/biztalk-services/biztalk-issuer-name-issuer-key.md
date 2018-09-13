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
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="29ae6-104">BizTalk Services: Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-104">BizTalk Services: Issuer Name and Issuer Key</span></span>
<span data-ttu-id="29ae6-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span><span class="sxs-lookup"><span data-stu-id="29ae6-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="29ae6-106">Specifically:</span><span class="sxs-lookup"><span data-stu-id="29ae6-106">Specifically:</span></span>

| <span data-ttu-id="29ae6-107">Task</span><span class="sxs-lookup"><span data-stu-id="29ae6-107">Task</span></span> | <span data-ttu-id="29ae6-108">Which Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="29ae6-109">Deploying your application from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29ae6-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="29ae6-110">Access Control Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="29ae6-111">Configuring the Azure BizTalk Services Portal</span><span class="sxs-lookup"><span data-stu-id="29ae6-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="29ae6-112">Access Control Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="29ae6-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29ae6-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="29ae6-114">Service Bus Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="29ae6-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span><span class="sxs-lookup"><span data-stu-id="29ae6-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="29ae6-116">Access Control Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="29ae6-117">The Access Control Issuer Name and Issuer Key are used by the following:</span><span class="sxs-lookup"><span data-stu-id="29ae6-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="29ae6-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span><span class="sxs-lookup"><span data-stu-id="29ae6-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="29ae6-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span><span class="sxs-lookup"><span data-stu-id="29ae6-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="29ae6-120">Get the Access Control Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="29ae6-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span><span class="sxs-lookup"><span data-stu-id="29ae6-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="29ae6-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="29ae6-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="29ae6-123">Add your Azure account: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="29ae6-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="29ae6-124">Return your subscription name: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="29ae6-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="29ae6-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="29ae6-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="29ae6-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="29ae6-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="29ae6-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="29ae6-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="29ae6-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span><span class="sxs-lookup"><span data-stu-id="29ae6-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

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

<span data-ttu-id="29ae6-129">To summarize:</span><span class="sxs-lookup"><span data-stu-id="29ae6-129">To summarize:</span></span>  
<span data-ttu-id="29ae6-130">Issuer Name = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="29ae6-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="29ae6-131">Issuer Key = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="29ae6-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="29ae6-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29ae6-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="29ae6-133">Service Bus Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="29ae6-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span><span class="sxs-lookup"><span data-stu-id="29ae6-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="29ae6-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span><span class="sxs-lookup"><span data-stu-id="29ae6-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="29ae6-136">To connect, you create the LOB Relay and enter your LOB system details.</span><span class="sxs-lookup"><span data-stu-id="29ae6-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="29ae6-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span><span class="sxs-lookup"><span data-stu-id="29ae6-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="29ae6-138">To retrieve the Service Bus Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="29ae6-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="29ae6-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="29ae6-140">In the left navigation pane, select **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="29ae6-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="29ae6-141">Select your namespace.</span><span class="sxs-lookup"><span data-stu-id="29ae6-141">Select your namespace.</span></span> <span data-ttu-id="29ae6-142">In the task bar, select **Connection Information**.</span><span class="sxs-lookup"><span data-stu-id="29ae6-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="29ae6-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span><span class="sxs-lookup"><span data-stu-id="29ae6-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="29ae6-144">Their values can be copied.</span><span class="sxs-lookup"><span data-stu-id="29ae6-144">Their values can be copied.</span></span>  

<span data-ttu-id="29ae6-145">To summarize:</span><span class="sxs-lookup"><span data-stu-id="29ae6-145">To summarize:</span></span>  
<span data-ttu-id="29ae6-146">Issuer Name = Default Issuer</span><span class="sxs-lookup"><span data-stu-id="29ae6-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="29ae6-147">Issuer Key = Default Key</span><span class="sxs-lookup"><span data-stu-id="29ae6-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="29ae6-148">Next</span><span class="sxs-lookup"><span data-stu-id="29ae6-148">Next</span></span>
<span data-ttu-id="29ae6-149">Additional Azure BizTalk Services topics:</span><span class="sxs-lookup"><span data-stu-id="29ae6-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="29ae6-150">Installing the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="29ae6-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="29ae6-151">Tutorials: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="29ae6-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="29ae6-152">How do I Start Using the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="29ae6-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="29ae6-153">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="29ae6-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="29ae6-154">See Also</span><span class="sxs-lookup"><span data-stu-id="29ae6-154">See Also</span></span>
* [<span data-ttu-id="29ae6-155">How to: Use ACS Management Service to Configure Service Identities</span><span class="sxs-lookup"><span data-stu-id="29ae6-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="29ae6-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span><span class="sxs-lookup"><span data-stu-id="29ae6-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="29ae6-157">BizTalk Services: Provisioning Using Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="29ae6-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="29ae6-158">BizTalk Services: Provisioning Status Chart</span><span class="sxs-lookup"><span data-stu-id="29ae6-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="29ae6-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="29ae6-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="29ae6-160">BizTalk Services: Backup and Restore</span><span class="sxs-lookup"><span data-stu-id="29ae6-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="29ae6-161">BizTalk Services: Throttling</span><span class="sxs-lookup"><span data-stu-id="29ae6-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

