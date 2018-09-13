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
# <a name="event-hubs-management-libraries"></a>Event Hubs management libraries

You can use the Azure Event Hubs management libraries to dynamically provision Event Hubs namespaces and entities. This dynamic nature enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision. These libraries are currently available for .NET.

## <a name="supported-functionality"></a>Supported functionality

* Namespace creation, update, deletion
* Event Hubs creation, update, deletion
* Consumer Group creation, update, deletion

## <a name="prerequisites"></a>Prerequisites

To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD). AAD requires that you authenticate as a service principal, which provides access to your Azure resources. For information about creating a service principal, see one of these articles:  

* [Use the Azure portal to create Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries. You must have **Owner** permissions for the resource group on which you want to run.

## <a name="programming-pattern"></a>Programming pattern

The pattern to manipulate any Event Hubs resource follows a common protocol:

1. Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Create the `EventHubManagementClient` object.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Set the `CreateOrUpdate` parameters to your specified values.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Execute the call.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Next steps
* [.NET Management sample](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Microsoft.Azure.Management.EventHub Reference](/dotnet/api/Microsoft.Azure.Management.EventHub) 
