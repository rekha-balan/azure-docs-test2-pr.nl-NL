---
title: How to manage your Azure Maps account and keys | Microsoft Docs
description: You can use the Azure portal to manage your Azure Maps account and manage your access keys.
author: dsk-2015
ms.author: dkshir
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: f5596f4c9bc827852c730d18856753e87de3c59c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865821"
---
# <a name="how-to-manage-your-azure-maps-account-and-keys"></a>How to manage your Azure Maps account and keys

You can manage your Azure Maps account and keys through the Azure portal. Once you have an account and a key, you can implement the APIs in your web site or mobile application.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## <a name="create-a-new-account"></a>Create a new account

1. Sign in to the [Azure portal](http://portal.azure.com).

1. Click **Create a resource** in the upper left-hand corner of the Azure portal.

2. Search for and select **Maps**, then click **Create**.

3. Enter the information for your new account. 

![Enter account information in the portal](./media/how-to-manage-account-keys/new-account-portal.png)

## <a name="manage-keys-on-the-account-page"></a>Manage keys on the account page

Once you create an account, you get two randomly generated keys. You use the keys to authenticate against the Maps APIs when you want to retrieve map data or create a new JavaScript map instance. 

You can find your keys in the Azure portal. Navigate to your account then select **Keys** from the menu.

![Manage account keys in the portal](./media/how-to-manage-account-keys/account-keys-portal.png)

From this page you can copy your keys or generate new ones. 

## <a name="delete-an-account"></a>Delete an account

You can delete an account from the Azure portal. Navigate to the account overview page and select **Delete**.

![Delete your account in the portal](./media/how-to-manage-account-keys/account-delete-portal.png)

## <a name="next-steps"></a>Next steps

* Learn how to use Azure Maps search APIs at [search for an address](./how-to-search-for-address.md).
* Learn how to use Azure maps [JavaScript map control](./how-to-use-map-control.md).
