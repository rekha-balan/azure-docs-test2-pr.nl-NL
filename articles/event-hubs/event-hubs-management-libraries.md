---
title: Azure Event Hubs management libraries | Microsoft Docs
description: Manage Event Hubs namespaces and entities from .NET
services: event-hubs
cloud: na
documentationcenter: na
author: jtaubensee
manager: timlt
ms.assetid: ''
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 4/10/2017
ms.author: jotaub;sethm
ms.openlocfilehash: a9023448c4ced1edf54c84bb103454cbd76fbfba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554062"
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="1a57f-103">Event Hubs management libraries</span><span class="sxs-lookup"><span data-stu-id="1a57f-103">Event Hubs management libraries</span></span>

<span data-ttu-id="1a57f-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span><span class="sxs-lookup"><span data-stu-id="1a57f-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="1a57f-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span><span class="sxs-lookup"><span data-stu-id="1a57f-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="1a57f-106">These libraries are currently available for .NET.</span><span class="sxs-lookup"><span data-stu-id="1a57f-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="1a57f-107">Supported functionality</span><span class="sxs-lookup"><span data-stu-id="1a57f-107">Supported functionality</span></span>

* <span data-ttu-id="1a57f-108">Namespace creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="1a57f-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="1a57f-109">Event Hubs creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="1a57f-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="1a57f-110">Consumer Group creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="1a57f-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a57f-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a57f-111">Prerequisites</span></span>

<span data-ttu-id="1a57f-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="1a57f-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="1a57f-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="1a57f-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="1a57f-114">For information about creating a service principal, see one of these articles:</span><span class="sxs-lookup"><span data-stu-id="1a57f-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="1a57f-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span><span class="sxs-lookup"><span data-stu-id="1a57f-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="1a57f-116">Use Azure PowerShell to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="1a57f-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="1a57f-117">Use Azure CLI to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="1a57f-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="1a57f-118">These tutorials will provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (Authentication Key), all of which are used for authentication by the management libraries.</span><span class="sxs-lookup"><span data-stu-id="1a57f-118">These tutorials will provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (Authentication Key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="1a57f-119">You must have 'Owner' permissions for the resource group on which you wish to run.</span><span class="sxs-lookup"><span data-stu-id="1a57f-119">You must have 'Owner' permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="1a57f-120">Programming pattern</span><span class="sxs-lookup"><span data-stu-id="1a57f-120">Programming pattern</span></span>

<span data-ttu-id="1a57f-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span><span class="sxs-lookup"><span data-stu-id="1a57f-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="1a57f-122">Obtain a token from Azure Active Directory using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span><span class="sxs-lookup"><span data-stu-id="1a57f-122">Obtain a token from Azure Active Directory using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.windows.net/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="1a57f-123">Create the `EventHubManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="1a57f-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="1a57f-124">Set the `CreateOrUpdate` parameters to your specified values.</span><span class="sxs-lookup"><span data-stu-id="1a57f-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="1a57f-125">Execute the call.</span><span class="sxs-lookup"><span data-stu-id="1a57f-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="1a57f-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a57f-126">Next steps</span></span>
* [<span data-ttu-id="1a57f-127">.NET Management sample</span><span class="sxs-lookup"><span data-stu-id="1a57f-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="1a57f-128">Microsoft.Azure.Management.EventHub Reference</span><span class="sxs-lookup"><span data-stu-id="1a57f-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
