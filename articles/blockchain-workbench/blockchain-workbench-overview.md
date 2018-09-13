---
title: Azure Blockchain Workbench overview
description: Overview of Azure Blockchain Workbench and its capabilities.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 3/21/2018
ms.topic: overview
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 9cd8ef3977d12364759838b46632ba32e0de6e70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867595"
---
# <a name="what-is-azure-blockchain-workbench"></a><span data-ttu-id="a48a0-103">What is Azure Blockchain Workbench?</span><span class="sxs-lookup"><span data-stu-id="a48a0-103">What is Azure Blockchain Workbench?</span></span>

<span data-ttu-id="a48a0-104">Azure Blockchain Workbench is a collection of Azure services and capabilities designed to help you create and deploy blockchain applications to share business processes and data with other organizations.</span><span class="sxs-lookup"><span data-stu-id="a48a0-104">Azure Blockchain Workbench is a collection of Azure services and capabilities designed to help you create and deploy blockchain applications to share business processes and data with other organizations.</span></span> <span data-ttu-id="a48a0-105">Azure Blockchain Workbench provides the infrastructure scaffolding for building blockchain applications enabling developers to focus on creating business logic and smart contracts.</span><span class="sxs-lookup"><span data-stu-id="a48a0-105">Azure Blockchain Workbench provides the infrastructure scaffolding for building blockchain applications enabling developers to focus on creating business logic and smart contracts.</span></span> <span data-ttu-id="a48a0-106">It also makes it easier to create blockchain applications by integrating several Azure services and capabilities to help automate common development tasks.</span><span class="sxs-lookup"><span data-stu-id="a48a0-106">It also makes it easier to create blockchain applications by integrating several Azure services and capabilities to help automate common development tasks.</span></span>

## <a name="create-blockchain-applications"></a><span data-ttu-id="a48a0-107">Create blockchain applications</span><span class="sxs-lookup"><span data-stu-id="a48a0-107">Create blockchain applications</span></span>

<span data-ttu-id="a48a0-108">With Blockchain Workbench, you can define blockchain applications using configuration and writing smart contract code.</span><span class="sxs-lookup"><span data-stu-id="a48a0-108">With Blockchain Workbench, you can define blockchain applications using configuration and writing smart contract code.</span></span> <span data-ttu-id="a48a0-109">You can jumpstart blockchain application development and focus on defining your contract and writing business logic instead of building scaffolding and setting up supporting services.</span><span class="sxs-lookup"><span data-stu-id="a48a0-109">You can jumpstart blockchain application development and focus on defining your contract and writing business logic instead of building scaffolding and setting up supporting services.</span></span>

## <a name="manage-applications-and-users"></a><span data-ttu-id="a48a0-110">Manage applications and users</span><span class="sxs-lookup"><span data-stu-id="a48a0-110">Manage applications and users</span></span>

<span data-ttu-id="a48a0-111">Azure Blockchain Workbench provides a web application and REST APIs for managing blockchain applications and users.</span><span class="sxs-lookup"><span data-stu-id="a48a0-111">Azure Blockchain Workbench provides a web application and REST APIs for managing blockchain applications and users.</span></span> <span data-ttu-id="a48a0-112">Blockchain Workbench administrators can manage application access and assign your users to application roles.</span><span class="sxs-lookup"><span data-stu-id="a48a0-112">Blockchain Workbench administrators can manage application access and assign your users to application roles.</span></span> <span data-ttu-id="a48a0-113">Azure AD users are automatically mapped to members in the application.</span><span class="sxs-lookup"><span data-stu-id="a48a0-113">Azure AD users are automatically mapped to members in the application.</span></span>

## <a name="integrate-blockchain-with-applications"></a><span data-ttu-id="a48a0-114">Integrate blockchain with applications</span><span class="sxs-lookup"><span data-stu-id="a48a0-114">Integrate blockchain with applications</span></span>

<span data-ttu-id="a48a0-115">You can use the Blockchain Workbench REST APIs and message-based APIs to integrate with existing systems.</span><span class="sxs-lookup"><span data-stu-id="a48a0-115">You can use the Blockchain Workbench REST APIs and message-based APIs to integrate with existing systems.</span></span> <span data-ttu-id="a48a0-116">The APIs provide an interface to allow for replacing or using multiple distributed ledger technologies, storage, and database offerings.</span><span class="sxs-lookup"><span data-stu-id="a48a0-116">The APIs provide an interface to allow for replacing or using multiple distributed ledger technologies, storage, and database offerings.</span></span>

<span data-ttu-id="a48a0-117">Blockchain Workbench can transform messages sent to its message-based API to build transactions in a format expected by that blockchain’s native API.</span><span class="sxs-lookup"><span data-stu-id="a48a0-117">Blockchain Workbench can transform messages sent to its message-based API to build transactions in a format expected by that blockchain’s native API.</span></span>  <span data-ttu-id="a48a0-118">Workbench can sign and route transactions to the appropriate blockchain.</span><span class="sxs-lookup"><span data-stu-id="a48a0-118">Workbench can sign and route transactions to the appropriate blockchain.</span></span> 

<span data-ttu-id="a48a0-119">Workbench automatically delivers events to Service Bus and Event Grid to send messages to downstream consumers.</span><span class="sxs-lookup"><span data-stu-id="a48a0-119">Workbench automatically delivers events to Service Bus and Event Grid to send messages to downstream consumers.</span></span> <span data-ttu-id="a48a0-120">Developers can integrate with either of these messaging systems to drive transactions and to look at results.</span><span class="sxs-lookup"><span data-stu-id="a48a0-120">Developers can integrate with either of these messaging systems to drive transactions and to look at results.</span></span>

## <a name="deploy-a-blockchain-network"></a><span data-ttu-id="a48a0-121">Deploy a blockchain network</span><span class="sxs-lookup"><span data-stu-id="a48a0-121">Deploy a blockchain network</span></span>

<span data-ttu-id="a48a0-122">Azure Blockchain Workbench simplifies consortium blockchain network setup as a preconfigured solution with an Azure Resource Manager solution template.</span><span class="sxs-lookup"><span data-stu-id="a48a0-122">Azure Blockchain Workbench simplifies consortium blockchain network setup as a preconfigured solution with an Azure Resource Manager solution template.</span></span> <span data-ttu-id="a48a0-123">The template provides simplified deployment that deploys all components needed to run a consortium.</span><span class="sxs-lookup"><span data-stu-id="a48a0-123">The template provides simplified deployment that deploys all components needed to run a consortium.</span></span> <span data-ttu-id="a48a0-124">Today, Blockchain Workbench currently supports Ethereum.</span><span class="sxs-lookup"><span data-stu-id="a48a0-124">Today, Blockchain Workbench currently supports Ethereum.</span></span>

## <a name="use-active-directory-login"></a><span data-ttu-id="a48a0-125">Use Active Directory login</span><span class="sxs-lookup"><span data-stu-id="a48a0-125">Use Active Directory login</span></span>

<span data-ttu-id="a48a0-126">With existing blockchain protocols, blockchain identities are represented as an address on the network.</span><span class="sxs-lookup"><span data-stu-id="a48a0-126">With existing blockchain protocols, blockchain identities are represented as an address on the network.</span></span> <span data-ttu-id="a48a0-127">Azure Blockchain Workbench abstracts away the blockchain identity by associating it with an Active Directory identity, making it simpler to build enterprise applications with Active Directory identities.</span><span class="sxs-lookup"><span data-stu-id="a48a0-127">Azure Blockchain Workbench abstracts away the blockchain identity by associating it with an Active Directory identity, making it simpler to build enterprise applications with Active Directory identities.</span></span>

## <a name="synchronize-on-chain-data-with-off-chain-storage"></a><span data-ttu-id="a48a0-128">Synchronize on-chain data with off-chain storage</span><span class="sxs-lookup"><span data-stu-id="a48a0-128">Synchronize on-chain data with off-chain storage</span></span>

<span data-ttu-id="a48a0-129">Azure Blockchain Workbench makes it easier to analyze blockchain events and data by automatically synchronizing data on the blockchain to off-chain storage.</span><span class="sxs-lookup"><span data-stu-id="a48a0-129">Azure Blockchain Workbench makes it easier to analyze blockchain events and data by automatically synchronizing data on the blockchain to off-chain storage.</span></span> <span data-ttu-id="a48a0-130">Instead of extracting data directly from the blockchain, you can query off-chain database systems such as SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a48a0-130">Instead of extracting data directly from the blockchain, you can query off-chain database systems such as SQL Server.</span></span> <span data-ttu-id="a48a0-131">Blockchain specific expertise is not required for end users who are doing data analysis tasks.</span><span class="sxs-lookup"><span data-stu-id="a48a0-131">Blockchain specific expertise is not required for end users who are doing data analysis tasks.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a48a0-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a48a0-132">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a48a0-133">Azure Blockchain Workbench architecture</span><span class="sxs-lookup"><span data-stu-id="a48a0-133">Azure Blockchain Workbench architecture</span></span>](blockchain-workbench-architecture.md)
