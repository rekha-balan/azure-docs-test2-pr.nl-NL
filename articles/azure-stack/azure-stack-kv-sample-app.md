---
title: Allow application to retrieve Azure Stack Key Vault secrets  | Microsoft Docs
description: Use a sample app to work with Azure Stack Key Vault
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: sngun
ms.openlocfilehash: 3d64805f30efe986c3be4408189ef823e5b72430
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671381"
---
# <a name="run-the-sample-application-for-key-vault"></a>Run the sample application for Key Vault
In this guide, you'll use a sample application to retrieve secrets and passwords from Key Vault.

> [!NOTE]
> In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only. If you are an administrator, sign in to the user portal to access and perform operations on a key vault.

## <a name="download-the-samples-and-prepare"></a>Download the samples and prepare
Download the Azure Key Vault client samples from the [Azure Key Vault client samples page](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Extract the contents of the .zip file to your local computer.

Read the **README.md** file (this is a text file), and then follow the instructions.

## <a name="run-sample-1--hellokeyvault"></a>Run Sample #1--HelloKeyVault
HelloKeyVault is a console application that walks through the key scenarios that are supported by Key Vault:

1. Create/import a key (HSM or software key)
2. Encrypt a secret using a content key
3. Wrap the content key using a Key Vault key
4. Unwrap the content key
5. Decrypt the secret
6. Set a secret

That console application should run with no changes, except that the appropriate configuration settings in App.Config will be updated according to the following steps:

1. Update the app configuration settings in HelloKeyVault\App.config with your vault URL, application principal ID, and secret. The information can optionally be generated using **scripts\GetAppConfigSettings.ps1**.
2. Update the values of the mandatory variables in GetAppConfigSettings.ps1.
3. Launch the Windows PowerShell window.
4. Run the GetAppConfigSettings.ps1 script within the PowerShell window.
5. Copy the results of the script to the HelloKeyVault\App.config file.

## <a name="next-steps"></a>Next steps
[Deploy a VM with a Key Vault password](azure-stack-kv-deploy-vm-with-secret.md)

[Deploy a VM with a Key Vault certificate](azure-stack-kv-push-secret-into-vm.md)

