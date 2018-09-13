---
title: Get the required values for authenticating an application to access SQL Database from code | Microsoft Docs
description: Create a service principal for accessing SQL Database from code.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: ''
tags: ''
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: development
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: 321b1630680f8bd4271f863b2cbe39be1a00cb89
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555784"
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a><span data-ttu-id="3e3c4-103">Get the required values for authenticating an application to access SQL Database from code</span><span class="sxs-lookup"><span data-stu-id="3e3c4-103">Get the required values for authenticating an application to access SQL Database from code</span></span>
<span data-ttu-id="3e3c4-104">To create and manage SQL Database from code you must register your app in the Azure Active Directory (AAD) domain  in the subscription where your Azure resources have been created.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-104">To create and manage SQL Database from code you must register your app in the Azure Active Directory (AAD) domain  in the subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a><span data-ttu-id="3e3c4-105">Create a service principal to access resources from an application</span><span class="sxs-lookup"><span data-stu-id="3e3c4-105">Create a service principal to access resources from an application</span></span>
<span data-ttu-id="3e3c4-106">You need to have the latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-106">You need to have the latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="3e3c4-107">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3e3c4-107">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="3e3c4-108">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-108">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="3e3c4-109">The script outputs values we need for the preceding C# sample.</span><span class="sxs-lookup"><span data-stu-id="3e3c4-109">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="3e3c4-110">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="3e3c4-110">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a><span data-ttu-id="3e3c4-111">See also</span><span class="sxs-lookup"><span data-stu-id="3e3c4-111">See also</span></span>
* [<span data-ttu-id="3e3c4-112">Create a SQL database with C#</span><span class="sxs-lookup"><span data-stu-id="3e3c4-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="3e3c4-113">Connecting to SQL Database By Using Azure Active Directory Authentication</span><span class="sxs-lookup"><span data-stu-id="3e3c4-113">Connecting to SQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

