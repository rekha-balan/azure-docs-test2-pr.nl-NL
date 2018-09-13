---
title: "Troubleshooting: 'Active Directory' item is missing or not available | Microsoft Docs"
description: What to do when Active Directory menu item doesn't appear in the Azure Management Portal.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: ''
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/07/2017
ms.author: mbaldwin
ms.openlocfilehash: f5a34ac7674ddb3c224e5b05dfdbea4df8ed5776
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670447"
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Troubleshooting: 'Active Directory' item is missing or not available
Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**." But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**? This topic is designed to help. It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.

## <a name="active-directory-is-missing"></a>Active Directory is missing
Typically, an **Active Directory** item appears in the left navigation menu. The instructions in Azure Active Directory procedures assume that this item is in your view.

![Screen shot: Active Directory in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-troubleshooting/typical-view.png)

The Active Directory item appears in the left navigation menu when any of the following conditions is true. Otherwise, the item does not appear.

* The current user signed on with a Microsoft account (formerly known as a Windows Live ID).
  
    OR
* The Azure tenant has a directory and the current account is a directory administrator.
  
    OR
* The Azure tenant has at least one Azure AD Access Control (ACS) namespace. For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OR
* The Azure tenant has at least one Azure Multi-Factor Authentication provider. For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.

To get administrative rights to a directory, have an administrator assign an administrator role to your account. For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory is not available
When you click **+New** > **App Services**, an **Active Directory** item appears. Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.

However, while the page is loading, the item is dimmed and is marked **Not Available**. This is a temporary state. If you wait a few seconds, the item becomes available. If the delay is prolonged, refreshing the web page often resolves the problem.

![Screen shot: Active Directory is not available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-troubleshooting/not-available.png)



