---
title: Export and delete your data from Machine Learning Studio - Azure | Microsoft Docs
description: In-product data stored by Azure Machine Learning Studio is available for export and deletion through the Azure portal and also through authenticated REST APIs. Telemetry data can be accessed through the Azure Privacy Portal. This article shows you how.
services: machine-learning
author: heatherbshapiro
ms.author: hshapiro
manager: cgronlun
ms.reviewer: jmartens, mldocs
ms.service: machine-learning
ms.component: studio
ms.topic: conceptual
ms.date: 05/25/2018
ms.openlocfilehash: 2ebd777a9723732de6ebbdf07020802190cb4b61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856604"
---
# <a name="export-and-delete-in-product-user-data-from-machine-learning-studio"></a>Export and delete in-product user data from Machine Learning Studio

You can delete or export in-product data stored by Azure Machine Learning Studio by using the Azure portal, the Studio interface, PowerShell, and authenticated REST APIs. This article tells you how. 

Telemetry data can be accessed through the Azure Privacy portal. 

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-dsr-and-stp-note.md)]

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

## <a name="what-kinds-of-user-data-does-studio-collect"></a>What kinds of user data does Studio collect?

For this service, user data consists of information about users authorized to access workspaces and telemetry records of user interactions with the service.

There are two kinds of user data in Machine Learning Studio:
- **Personal account data:** Account IDs and email addresses associated with an account.
- **Customer data:** Data you uploaded to analyze.

## <a name="studio-account-types-and-how-data-is-stored"></a>Studio account types and how data is stored

There are three kinds of accounts in Machine Learning Studio. The kind of account you have determines how your data is stored and how you can delete or export it.

- A **guest workspace** is a free, anonymous account. You sign up without providing credentials, such as an email address or password.
    -  Data is purged after the guest workspace expires.
    - Guest users can export customer data through the UI, REST APIs, or PowerShell package.
- A **free workspace** is a free account you sign in to with Microsoft account credentials - an email address and password.
    - You can export and delete personal and customer data, which are subject to data subject rights (DSR) requests.
    - You can export customer data through the UI, REST APIs, or PowerShell package.
    - For free workspaces not using Azure AD accounts, telemetry can be exported using the Privacy Portal.
    - When you delete the workspace, you delete all personal customer data.
- A **standard workspace** is a paid account you access with sign-in credentials.
    - You can export and delete personal and customer data, which are subject to DSR requests.
    - You can access data through the Azure Privacy portal
    - You can export personal and customer data through the UI, REST APIs, or PowerShell package
    - You can delete your data in the Azure portal.

## <a name="delete-workspace-data-in-studio"></a>Delete workspace data in Studio 

### <a name="delete-individual-assets"></a>Delete individual assets

Users can delete assets in a workspace by selecting them, and then selecting the delete button.

![Delete assets in Machine Learning Studio](./media/export-delete-personal-data-dsr/delete-studio-asset.png)

### <a name="delete-an-entire-workspace"></a>Delete an entire workspace

Users can also delete their entire workspace:
- Paid workspace: Delete through the Azure portal.
- Free workspace: Use the delete button in the **Settings** pane.

![Delete a free workspace in Machine Learning Studio](./media/export-delete-personal-data-dsr/delete-studio-data-workspace.png)
 
## <a name="export-studio-data-with-powershell"></a>Export Studio data with PowerShell
Use PowerShell to export all your information to a portable format from Azure Machine Learning Studio using commands. For information, see the [PowerShell module for Azure Machine Learning](powershell-module.md) article.

## <a name="next-steps"></a>Next steps

For documentation covering web services and commitment plan billing, see [Azure Machine Learning REST API reference](https://docs.microsoft.com/rest/api/machinelearning/). 
