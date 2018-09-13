---
title: Azure Event Hubs management libraries | Microsoft Docs
description: Manage Event Hubs namespaces and entities from .NET
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.date: 08/13/2018
ms.author: shvija
ms.openlocfilehash: 79cddcac4d469753bc39107e6db2d8ce901111d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824283"
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="f6e6b-103">Event Hubs management libraries</span><span class="sxs-lookup"><span data-stu-id="f6e6b-103">Event Hubs management libraries</span></span>

<span data-ttu-id="f6e6b-104">You can use the Azure Event Hubs management libraries to dynamically provision Event Hubs namespaces and entities.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-104">You can use the Azure Event Hubs management libraries to dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="f6e6b-105">This dynamic nature enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-105">This dynamic nature enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="f6e6b-106">These libraries are currently available for .NET.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="f6e6b-107">Supported functionality</span><span class="sxs-lookup"><span data-stu-id="f6e6b-107">Supported functionality</span></span>

* <span data-ttu-id="f6e6b-108">Namespace creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="f6e6b-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="f6e6b-109">Event Hubs creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="f6e6b-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="f6e6b-110">Consumer Group creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="f6e6b-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6e6b-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f6e6b-111">Prerequisites</span></span>

<span data-ttu-id="f6e6b-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="f6e6b-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="f6e6b-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="f6e6b-114">For information about creating a service principal, see one of these articles:</span><span class="sxs-lookup"><span data-stu-id="f6e6b-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="f6e6b-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span><span class="sxs-lookup"><span data-stu-id="f6e6b-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="f6e6b-116">Use Azure PowerShell to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="f6e6b-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="f6e6b-117">Use Azure CLI to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="f6e6b-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="f6e6b-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="f6e6b-119">You must have **Owner** permissions for the resource group on which you want to run.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="f6e6b-120">Programming pattern</span><span class="sxs-lookup"><span data-stu-id="f6e6b-120">Programming pattern</span></span>

<span data-ttu-id="f6e6b-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span><span class="sxs-lookup"><span data-stu-id="f6e6b-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="f6e6b-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="f6e6b-123">Create the `EventHubManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="f6e6b-124">Set the `CreateOrUpdate` parameters to your specified values.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="f6e6b-125">Execute the call.</span><span class="sxs-lookup"><span data-stu-id="f6e6b-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="f6e6b-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6e6b-126">Next steps</span></span>
* [<span data-ttu-id="f6e6b-127">.NET Management sample</span><span class="sxs-lookup"><span data-stu-id="f6e6b-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="f6e6b-128">Microsoft.Azure.Management.EventHub Reference</span><span class="sxs-lookup"><span data-stu-id="f6e6b-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
