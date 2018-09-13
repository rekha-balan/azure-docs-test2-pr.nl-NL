---
title: Use Azure CLI to create an Azure AD app and configure it to access Azure Media Services API | Microsoft Docs
description: This topic shows how to use the Azure CLI to create an Azure AD app and configure it to access Azure Media Services API.
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
ms.openlocfilehash: fcd0ea10bd39f9e7252e114e8d6401a4fe0ecadb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865952"
---
# <a name="use-azure-cli-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a>Use Azure CLI to create an AAD app and configure it to access Azure Media Services API

This topic shows you how to use the Azure CLI to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources. 

## <a name="prerequisites"></a>Prerequisites

- An Azure account. For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/). 
- A Media Services account. For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).

## <a name="use-the-azure-cloud-shell"></a>Use the Azure Cloud Shell

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Launch the Cloud Shell from the upper navigation pane of the portal.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

For more information, see [Overview of Azure Cloud Shell](../../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-azure-cli"></a>Create an Azure AD app and configure access to the media account with Azure CLI
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create --assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

For example:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

In this example, the **scope** is the full resource path for the media services account. However, the **scope** can be at any level.

For example, it could be one of the following levels:
 
* The **subscription** level.
* The **resource group** level.
* The **resource** level (for example, a Media account).

For more information, see [Create an Azure service principal with the Azure CLI](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Also see [Manage Role-Based Access Control with the Azure command-line interface](../../role-based-access-control/role-assignments-cli.md). 

## <a name="next-steps"></a>Next steps

Get started with [uploading files to your account](media-services-portal-upload-files.md).