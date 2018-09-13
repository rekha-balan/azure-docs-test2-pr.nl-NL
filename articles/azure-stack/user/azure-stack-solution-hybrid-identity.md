---
title: Configure hybrid cloud identity with Azure and Azure Stack applications | Microsoft Docs
description: Learn how to configure hybrid cloud identity with Azure and Azure Stack applications.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 05/22/2018
ms.author: mabrigg
ms.reviewer: Anjay.Ajodha
ms.openlocfilehash: a57afb4a90da5877879afddc35545e0bfef622a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857590"
---
# <a name="tutorial-configure-hybrid-cloud-identity-for-azure-and-azure-stack-applications"></a>Tutorial: configure hybrid cloud identity for Azure and Azure Stack applications

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

Learn how to configure a hybrid cloud identity for your Azure and Azure Stack applications.

You have two options for granting access to your applications in both global Azure and Azure Stack.

 * When Azure Stack has a continuous connection to the Internet, you can use Azure Active Directory (Azure AD).
 * When Azure Stack is disconnected from the Internet, you can use Azure Directory Federated Services (AD FS).

You use service principals to grant access to your Azure Stack applications for the purpose of deployment or configuration using the Azure Resource Manager in Azure Stack.

In this tutorial, you will build a sample environment to:

> [!div class="checklist"]
> * Establish a hybrid identity in global Azure and Azure Stack
> * Retrieve a token to access the Azure Stack API.

You must have Azure Stack operator permissions for the steps in this tutorial.

## <a name="create-a-service-principal-for-azure-ad-in-the-portal"></a>Create a service principal for Azure AD in the portal

If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure. The [create service principals](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-azure-ad) article shows you how to perform the steps through the portal. Check to see that you have the [required Azure AD permissions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions) before beginning.

## <a name="create-a-service-principal-for-ad-fs-using-powershell"></a>Create a service principal for AD FS using PowerShell

If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity. [Create service principal for AD FS](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-ad-fs) shows you how to perform the required steps using PowerShell.

## <a name="using-the-azure-stack-api"></a>Using the Azure Stack API

The [Azure Stack API](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-rest-api-use) tutorial walks you through the process of retrieving a token to access the Azure Stack API.

## <a name="connect-to-azure-stack-using-powershell"></a>Connect to Azure Stack using Powershell

The quickstart [to get up and running with PowerShell in Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart) walks you through the steps needed to install Azure PowerShell and connect to your Azure Stack installation.

### <a name="prerequisites"></a>Prerequisites

An Azure Stack installation connected to Azure Active Directory with a subscription you can access. If you don’t have an Azure Stack installation, you can use these instructions to set up an [Azure Stack Development Kit](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy).

#### <a name="connect-to-azure-stack-using-code"></a>Connect to Azure Stack using code

To connect to Azure Stack using code, use the Azure Resource Manager endpoints API to get the authentication and graph endpoints for your Azure Stack installation, and then authenticate using REST requests. You can find a sample client application on [GitHub](https://github.com/shriramnat/HybridARMApplication).

>[!Note]
>Unless the Azure SDK for your language of choice supports Azure API Profiles, the SDK may not work with Azure Stack. To learn more about Azure API Profiles, see the [manage API version profiles](https://docs.microsoft.com/da-dk/azure/azure-stack/user/azure-stack-version-profiles) article.

## <a name="next-steps"></a>Next steps

 - To learn more about how identity is handled in Azure Stack, see [Identity architecture for Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-architecture).
 - To learn more about Azure Cloud Patterns, see [Cloud Design Patterns](https://docs.microsoft.com/azure/architecture/patterns).
