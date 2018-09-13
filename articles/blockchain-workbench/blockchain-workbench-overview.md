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
# <a name="what-is-azure-blockchain-workbench"></a>What is Azure Blockchain Workbench?

Azure Blockchain Workbench is a collection of Azure services and capabilities designed to help you create and deploy blockchain applications to share business processes and data with other organizations. Azure Blockchain Workbench provides the infrastructure scaffolding for building blockchain applications enabling developers to focus on creating business logic and smart contracts. It also makes it easier to create blockchain applications by integrating several Azure services and capabilities to help automate common development tasks.

## <a name="create-blockchain-applications"></a>Create blockchain applications

With Blockchain Workbench, you can define blockchain applications using configuration and writing smart contract code. You can jumpstart blockchain application development and focus on defining your contract and writing business logic instead of building scaffolding and setting up supporting services.

## <a name="manage-applications-and-users"></a>Manage applications and users

Azure Blockchain Workbench provides a web application and REST APIs for managing blockchain applications and users. Blockchain Workbench administrators can manage application access and assign your users to application roles. Azure AD users are automatically mapped to members in the application.

## <a name="integrate-blockchain-with-applications"></a>Integrate blockchain with applications

You can use the Blockchain Workbench REST APIs and message-based APIs to integrate with existing systems. The APIs provide an interface to allow for replacing or using multiple distributed ledger technologies, storage, and database offerings.

Blockchain Workbench can transform messages sent to its message-based API to build transactions in a format expected by that blockchain’s native API.  Workbench can sign and route transactions to the appropriate blockchain. 

Workbench automatically delivers events to Service Bus and Event Grid to send messages to downstream consumers. Developers can integrate with either of these messaging systems to drive transactions and to look at results.

## <a name="deploy-a-blockchain-network"></a>Deploy a blockchain network

Azure Blockchain Workbench simplifies consortium blockchain network setup as a preconfigured solution with an Azure Resource Manager solution template. The template provides simplified deployment that deploys all components needed to run a consortium. Today, Blockchain Workbench currently supports Ethereum.

## <a name="use-active-directory-login"></a>Use Active Directory login

With existing blockchain protocols, blockchain identities are represented as an address on the network. Azure Blockchain Workbench abstracts away the blockchain identity by associating it with an Active Directory identity, making it simpler to build enterprise applications with Active Directory identities.

## <a name="synchronize-on-chain-data-with-off-chain-storage"></a>Synchronize on-chain data with off-chain storage

Azure Blockchain Workbench makes it easier to analyze blockchain events and data by automatically synchronizing data on the blockchain to off-chain storage. Instead of extracting data directly from the blockchain, you can query off-chain database systems such as SQL Server. Blockchain specific expertise is not required for end users who are doing data analysis tasks. 

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Azure Blockchain Workbench architecture](blockchain-workbench-architecture.md)
