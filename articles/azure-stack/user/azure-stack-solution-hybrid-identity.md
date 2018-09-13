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
# <a name="tutorial-configure-hybrid-cloud-identity-for-azure-and-azure-stack-applications"></a><span data-ttu-id="99f27-103">Tutorial: configure hybrid cloud identity for Azure and Azure Stack applications</span><span class="sxs-lookup"><span data-stu-id="99f27-103">Tutorial: configure hybrid cloud identity for Azure and Azure Stack applications</span></span>

<span data-ttu-id="99f27-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="99f27-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="99f27-105">Learn how to configure a hybrid cloud identity for your Azure and Azure Stack applications.</span><span class="sxs-lookup"><span data-stu-id="99f27-105">Learn how to configure a hybrid cloud identity for your Azure and Azure Stack applications.</span></span>

<span data-ttu-id="99f27-106">You have two options for granting access to your applications in both global Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99f27-106">You have two options for granting access to your applications in both global Azure and Azure Stack.</span></span>

 * <span data-ttu-id="99f27-107">When Azure Stack has a continuous connection to the Internet, you can use Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99f27-107">When Azure Stack has a continuous connection to the Internet, you can use Azure Active Directory (Azure AD).</span></span>
 * <span data-ttu-id="99f27-108">When Azure Stack is disconnected from the Internet, you can use Azure Directory Federated Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="99f27-108">When Azure Stack is disconnected from the Internet, you can use Azure Directory Federated Services (AD FS).</span></span>

<span data-ttu-id="99f27-109">You use service principals to grant access to your Azure Stack applications for the purpose of deployment or configuration using the Azure Resource Manager in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99f27-109">You use service principals to grant access to your Azure Stack applications for the purpose of deployment or configuration using the Azure Resource Manager in Azure Stack.</span></span>

<span data-ttu-id="99f27-110">In this tutorial, you will build a sample environment to:</span><span class="sxs-lookup"><span data-stu-id="99f27-110">In this tutorial, you will build a sample environment to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99f27-111">Establish a hybrid identity in global Azure and Azure Stack</span><span class="sxs-lookup"><span data-stu-id="99f27-111">Establish a hybrid identity in global Azure and Azure Stack</span></span>
> * <span data-ttu-id="99f27-112">Retrieve a token to access the Azure Stack API.</span><span class="sxs-lookup"><span data-stu-id="99f27-112">Retrieve a token to access the Azure Stack API.</span></span>

<span data-ttu-id="99f27-113">You must have Azure Stack operator permissions for the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="99f27-113">You must have Azure Stack operator permissions for the steps in this tutorial.</span></span>

## <a name="create-a-service-principal-for-azure-ad-in-the-portal"></a><span data-ttu-id="99f27-114">Create a service principal for Azure AD in the portal</span><span class="sxs-lookup"><span data-stu-id="99f27-114">Create a service principal for Azure AD in the portal</span></span>

<span data-ttu-id="99f27-115">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span><span class="sxs-lookup"><span data-stu-id="99f27-115">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span></span> <span data-ttu-id="99f27-116">The [create service principals](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-azure-ad) article shows you how to perform the steps through the portal.</span><span class="sxs-lookup"><span data-stu-id="99f27-116">The [create service principals](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-azure-ad) article shows you how to perform the steps through the portal.</span></span> <span data-ttu-id="99f27-117">Check to see that you have the [required Azure AD permissions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions) before beginning.</span><span class="sxs-lookup"><span data-stu-id="99f27-117">Check to see that you have the [required Azure AD permissions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions) before beginning.</span></span>

## <a name="create-a-service-principal-for-ad-fs-using-powershell"></a><span data-ttu-id="99f27-118">Create a service principal for AD FS using PowerShell</span><span class="sxs-lookup"><span data-stu-id="99f27-118">Create a service principal for AD FS using PowerShell</span></span>

<span data-ttu-id="99f27-119">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span><span class="sxs-lookup"><span data-stu-id="99f27-119">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span> <span data-ttu-id="99f27-120">[Create service principal for AD FS](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-ad-fs) shows you how to perform the required steps using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99f27-120">[Create service principal for AD FS](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-ad-fs) shows you how to perform the required steps using PowerShell.</span></span>

## <a name="using-the-azure-stack-api"></a><span data-ttu-id="99f27-121">Using the Azure Stack API</span><span class="sxs-lookup"><span data-stu-id="99f27-121">Using the Azure Stack API</span></span>

<span data-ttu-id="99f27-122">The [Azure Stack API](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-rest-api-use) tutorial walks you through the process of retrieving a token to access the Azure Stack API.</span><span class="sxs-lookup"><span data-stu-id="99f27-122">The [Azure Stack API](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-rest-api-use) tutorial walks you through the process of retrieving a token to access the Azure Stack API.</span></span>

## <a name="connect-to-azure-stack-using-powershell"></a><span data-ttu-id="99f27-123">Connect to Azure Stack using Powershell</span><span class="sxs-lookup"><span data-stu-id="99f27-123">Connect to Azure Stack using Powershell</span></span>

<span data-ttu-id="99f27-124">The quickstart [to get up and running with PowerShell in Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart) walks you through the steps needed to install Azure PowerShell and connect to your Azure Stack installation.</span><span class="sxs-lookup"><span data-stu-id="99f27-124">The quickstart [to get up and running with PowerShell in Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart) walks you through the steps needed to install Azure PowerShell and connect to your Azure Stack installation.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="99f27-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99f27-125">Prerequisites</span></span>

<span data-ttu-id="99f27-126">An Azure Stack installation connected to Azure Active Directory with a subscription you can access.</span><span class="sxs-lookup"><span data-stu-id="99f27-126">An Azure Stack installation connected to Azure Active Directory with a subscription you can access.</span></span> <span data-ttu-id="99f27-127">If you don’t have an Azure Stack installation, you can use these instructions to set up an [Azure Stack Development Kit](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy).</span><span class="sxs-lookup"><span data-stu-id="99f27-127">If you don’t have an Azure Stack installation, you can use these instructions to set up an [Azure Stack Development Kit](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy).</span></span>

#### <a name="connect-to-azure-stack-using-code"></a><span data-ttu-id="99f27-128">Connect to Azure Stack using code</span><span class="sxs-lookup"><span data-stu-id="99f27-128">Connect to Azure Stack using code</span></span>

<span data-ttu-id="99f27-129">To connect to Azure Stack using code, use the Azure Resource Manager endpoints API to get the authentication and graph endpoints for your Azure Stack installation, and then authenticate using REST requests.</span><span class="sxs-lookup"><span data-stu-id="99f27-129">To connect to Azure Stack using code, use the Azure Resource Manager endpoints API to get the authentication and graph endpoints for your Azure Stack installation, and then authenticate using REST requests.</span></span> <span data-ttu-id="99f27-130">You can find a sample client application on [GitHub](https://github.com/shriramnat/HybridARMApplication).</span><span class="sxs-lookup"><span data-stu-id="99f27-130">You can find a sample client application on [GitHub](https://github.com/shriramnat/HybridARMApplication).</span></span>

>[!Note]
><span data-ttu-id="99f27-131">Unless the Azure SDK for your language of choice supports Azure API Profiles, the SDK may not work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99f27-131">Unless the Azure SDK for your language of choice supports Azure API Profiles, the SDK may not work with Azure Stack.</span></span> <span data-ttu-id="99f27-132">To learn more about Azure API Profiles, see the [manage API version profiles](https://docs.microsoft.com/da-dk/azure/azure-stack/user/azure-stack-version-profiles) article.</span><span class="sxs-lookup"><span data-stu-id="99f27-132">To learn more about Azure API Profiles, see the [manage API version profiles](https://docs.microsoft.com/da-dk/azure/azure-stack/user/azure-stack-version-profiles) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99f27-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="99f27-133">Next steps</span></span>

 - <span data-ttu-id="99f27-134">To learn more about how identity is handled in Azure Stack, see [Identity architecture for Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-architecture).</span><span class="sxs-lookup"><span data-stu-id="99f27-134">To learn more about how identity is handled in Azure Stack, see [Identity architecture for Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-architecture).</span></span>
 - <span data-ttu-id="99f27-135">To learn more about Azure Cloud Patterns, see [Cloud Design Patterns](https://docs.microsoft.com/azure/architecture/patterns).</span><span class="sxs-lookup"><span data-stu-id="99f27-135">To learn more about Azure Cloud Patterns, see [Cloud Design Patterns](https://docs.microsoft.com/azure/architecture/patterns).</span></span>
