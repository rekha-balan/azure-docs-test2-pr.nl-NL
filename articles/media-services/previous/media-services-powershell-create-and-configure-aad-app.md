---
title: Use PowerShell to create an Azure AD app to access the Azure Media Services API | Microsoft Docs
description: Learn how to use PowerShell to create an Azure Active Directory (Azure AD) app and set it up to access the Azure Media Services API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 36f00c2b794730ae8191238c516cfedf871851bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870672"
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a>Use PowerShell to create an Azure AD app to use with the Azure Media Services API

Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.  

## <a name="prerequisites"></a>Prerequisites

- An Azure account. If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/). 
- A Media Services account. For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).
- Azure PowerShell version 0.8.8 or a later version. For more information, see [How to use Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Azure Resource Manager cmdlets.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Create an Azure AD app by using PowerShell  

```powershell
Connect-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

For more information, see the following articles:

- [Use Azure PowerShell to create a service principal to access resources](../../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Manage Role-Based Access Control by using Azure PowerShell](../../role-based-access-control/role-assignments-powershell.md)
- [How to manually configure daemon apps by using certificates](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Next steps

Get started with [uploading files to your account](media-services-portal-upload-files.md).
