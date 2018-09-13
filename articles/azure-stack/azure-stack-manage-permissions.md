---
title: Manage permissions to resources per user in Azure Stack (service administrator and tenant) | Microsoft Docs
description: As a service administrator or tenant, learn how to manage RBAC permissions.
services: azure-stack
documentationcenter: ''
author: Heathl17
manager: byronr
editor: ''
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: helaw
ms.openlocfilehash: caf9a6790039a9da1cc91d6566c196da41667713
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671336"
---
# <a name="manage-role-based-access-control"></a>Manage Role-Based Access Control
A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service. For example, User A might have reader permissions to Subscription 1, but have owner permissions to Virtual Machine 7.

* Reader: User can view everything, but can’t make any changes.
* Contributor: User can manage everything except access to resources.
* Owner: User can manage everything, including access to resources.

## <a name="set-access-permissions-for-a-user"></a>Set access permissions for a user
1. Sign in with an account that has owner permissions to the resource you want to manage.
2. In the blade for the resource, click the **Access** icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-permissions/image1.png).
3. In the **Users** blade, click **Roles**.
4. In the **Roles** blade, click **Add** to add permissions for the user.

## <a name="next-steps"></a>Next steps
[Add an Azure Stack tenant](azure-stack-add-new-user-aad.md)

