---
title: Azure Service Bus management libraries| Microsoft Docs
description: Manage Service Bus namespaces and messaging entities from .NET
services: service-bus-messaging
cloud: na
documentationcenter: na
author: jtaubensee
manager: timlt
ms.assetid: ''
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: jotaub;sethm
ms.openlocfilehash: ec9f2fa3d88f59172d320b58287208deb084856f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553509"
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="8b340-103">Service Bus management libraries</span><span class="sxs-lookup"><span data-stu-id="8b340-103">Service Bus management libraries</span></span>

<span data-ttu-id="8b340-104">The Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span><span class="sxs-lookup"><span data-stu-id="8b340-104">The Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="8b340-105">This allows for complex deployments and messaging scenarios, enabling you to programmatically determine what entities to provision.</span><span class="sxs-lookup"><span data-stu-id="8b340-105">This allows for complex deployments and messaging scenarios, enabling you to programmatically determine what entities to provision.</span></span> <span data-ttu-id="8b340-106">These libraries are currently available for .NET.</span><span class="sxs-lookup"><span data-stu-id="8b340-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="8b340-107">Supported functionality</span><span class="sxs-lookup"><span data-stu-id="8b340-107">Supported functionality</span></span>

* <span data-ttu-id="8b340-108">Namespace creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="8b340-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="8b340-109">Queue creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="8b340-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="8b340-110">Topic creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="8b340-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="8b340-111">Subscription creation, update, deletion</span><span class="sxs-lookup"><span data-stu-id="8b340-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b340-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b340-112">Prerequisites</span></span>

<span data-ttu-id="8b340-113">To get started using the Service Bus management libraries, you must authenticate with Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8b340-113">To get started using the Service Bus management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="8b340-114">AAD requires that you authenticate as a service principal which provides access to your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8b340-114">AAD requires that you authenticate as a service principal which provides access to your Azure resources.</span></span> <span data-ttu-id="8b340-115">For information about creating a service principal, see one of these articles:</span><span class="sxs-lookup"><span data-stu-id="8b340-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="8b340-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span><span class="sxs-lookup"><span data-stu-id="8b340-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="8b340-117">Use Azure PowerShell to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="8b340-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="8b340-118">Use Azure CLI to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="8b340-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="8b340-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span><span class="sxs-lookup"><span data-stu-id="8b340-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="8b340-120">You must have 'Owner' permissions for the resource group on which you wish to run.</span><span class="sxs-lookup"><span data-stu-id="8b340-120">You must have 'Owner' permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="8b340-121">Programming pattern</span><span class="sxs-lookup"><span data-stu-id="8b340-121">Programming pattern</span></span>

<span data-ttu-id="8b340-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span><span class="sxs-lookup"><span data-stu-id="8b340-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="8b340-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span><span class="sxs-lookup"><span data-stu-id="8b340-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.windows.net/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="8b340-124">Create the `ServiceBusManagementClient` object.</span><span class="sxs-lookup"><span data-stu-id="8b340-124">Create the `ServiceBusManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var sbClient = new ServiceBusManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="8b340-125">Set the `CreateOrUpdate` parameters to your specified values.</span><span class="sxs-lookup"><span data-stu-id="8b340-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var queueParams = new QueueCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"],
        EnablePartitioning = true
    };
    ```

1. <span data-ttu-id="8b340-126">Execute the call.</span><span class="sxs-lookup"><span data-stu-id="8b340-126">Execute the call.</span></span>
    ```csharp
    await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="8b340-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b340-127">Next steps</span></span>
* [<span data-ttu-id="8b340-128">.NET Management sample</span><span class="sxs-lookup"><span data-stu-id="8b340-128">.NET Management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="8b340-129">Microsoft.Azure.Management.ServiceBus Reference</span><span class="sxs-lookup"><span data-stu-id="8b340-129">Microsoft.Azure.Management.ServiceBus Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
