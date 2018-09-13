---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 70a9e2a8f6327c0af92698b49d5b622bebba3661
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968590"
---
1. Sign in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions. For more information about signing in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

  ```azurecli
  az login
  ```
2. If you have more than one Azure subscription, list the subscriptions for the account.

  ```azurecli
  az account list --all
  ```
3. Specify the subscription that you want to use.

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```