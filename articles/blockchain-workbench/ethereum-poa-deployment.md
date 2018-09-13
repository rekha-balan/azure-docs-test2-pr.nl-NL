---
title: Ethereum Proof-of-Authority Consortium
description: Use the Etherereum Proof-of-Authority Consortium solution to deploy and configure a multi-member consortium Ethereum network
services: azure-blockchain
keywords: ''
author: CodyBorn
ms.author: coborn
ms.date: 8/2/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: brendal
manager: vamelech
ms.openlocfilehash: fcb35f23be384b3625e4e17e5dc2285b7eeb341a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869433"
---
# <a name="ethereum-proof-of-authority-consortium"></a><span data-ttu-id="4f8bc-103">Ethereum proof-of-authority consortium</span><span class="sxs-lookup"><span data-stu-id="4f8bc-103">Ethereum proof-of-authority consortium</span></span>

<span data-ttu-id="4f8bc-104">[This solution](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) is designed to make it easier to deploy, configure, and govern a multi-member consortium Proof-of-authority Ethereum network with minimal Azure and Ethereum knowledge.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-104">[This solution](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) is designed to make it easier to deploy, configure, and govern a multi-member consortium Proof-of-authority Ethereum network with minimal Azure and Ethereum knowledge.</span></span>

<span data-ttu-id="4f8bc-105">With a handful of user inputs and a single-click deployment through the Azure portal, each member can provision a network footprint, using Microsoft Azure Compute, networking, and storage services across the globe.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-105">With a handful of user inputs and a single-click deployment through the Azure portal, each member can provision a network footprint, using Microsoft Azure Compute, networking, and storage services across the globe.</span></span> <span data-ttu-id="4f8bc-106">Each member's network footprint consists of a set of load-balanced validator nodes with which an application or user can interact to submit Ethereum transactions.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-106">Each member's network footprint consists of a set of load-balanced validator nodes with which an application or user can interact to submit Ethereum transactions.</span></span>

## <a name="concepts"></a><span data-ttu-id="4f8bc-107">Concepts</span><span class="sxs-lookup"><span data-stu-id="4f8bc-107">Concepts</span></span>

### <a name="terminology"></a><span data-ttu-id="4f8bc-108">Terminology</span><span class="sxs-lookup"><span data-stu-id="4f8bc-108">Terminology</span></span>

-   <span data-ttu-id="4f8bc-109">**Consensus** - The act of synchronizing data across the distributed network through block validation and creation.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-109">**Consensus** - The act of synchronizing data across the distributed network through block validation and creation.</span></span>

-   <span data-ttu-id="4f8bc-110">**Consortium member** - An entity that participates in consensus on the Blockchain network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-110">**Consortium member** - An entity that participates in consensus on the Blockchain network.</span></span>

-   <span data-ttu-id="4f8bc-111">**Admin** - An Ethereum account that is used to manage participation for a given consortium member.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-111">**Admin** - An Ethereum account that is used to manage participation for a given consortium member.</span></span>

-   <span data-ttu-id="4f8bc-112">**Validator** - A machine associated with an Ethereum account that participates in consensus on behalf of an Admin.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-112">**Validator** - A machine associated with an Ethereum account that participates in consensus on behalf of an Admin.</span></span>

### <a name="proof-of-authority"></a><span data-ttu-id="4f8bc-113">Proof-of-authority</span><span class="sxs-lookup"><span data-stu-id="4f8bc-113">Proof-of-authority</span></span>

<span data-ttu-id="4f8bc-114">For those of you who are new to the blockchain community, the release of this solution is a great opportunity to learn about the technology in an easy and configurable manner on Azure.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-114">For those of you who are new to the blockchain community, the release of this solution is a great opportunity to learn about the technology in an easy and configurable manner on Azure.</span></span> <span data-ttu-id="4f8bc-115">Proof-of-work is a Sybil-resistance mechanism that leverages computation costs to self-regulate the network and allow fair participation.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-115">Proof-of-work is a Sybil-resistance mechanism that leverages computation costs to self-regulate the network and allow fair participation.</span></span> <span data-ttu-id="4f8bc-116">This works great in anonymous, open blockchain networks where competition for cryptocurrency promotes security on the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-116">This works great in anonymous, open blockchain networks where competition for cryptocurrency promotes security on the network.</span></span> <span data-ttu-id="4f8bc-117">However, in private/consortium networks the underlying Ether has no value.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-117">However, in private/consortium networks the underlying Ether has no value.</span></span> <span data-ttu-id="4f8bc-118">An alternative protocol, proof-of-authority, is more suitable for permissioned networks where all consensus participants are known and reputable.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-118">An alternative protocol, proof-of-authority, is more suitable for permissioned networks where all consensus participants are known and reputable.</span></span> <span data-ttu-id="4f8bc-119">Without the need for mining, Proof-of-authority is more efficient while still retaining Byzantine fault tolerance.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-119">Without the need for mining, Proof-of-authority is more efficient while still retaining Byzantine fault tolerance.</span></span>

### <a name="consortium-governance"></a><span data-ttu-id="4f8bc-120">Consortium governance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-120">Consortium governance</span></span>

<span data-ttu-id="4f8bc-121">Since proof-of-authority relies upon a permissioned list of network authorities to keep the network healthy, it's important to provide a fair mechanism to make modifications to this permission list.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-121">Since proof-of-authority relies upon a permissioned list of network authorities to keep the network healthy, it's important to provide a fair mechanism to make modifications to this permission list.</span></span> <span data-ttu-id="4f8bc-122">Each deployment comes with a set of smart-contracts and portal for on-chain governance of this permissioned list.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-122">Each deployment comes with a set of smart-contracts and portal for on-chain governance of this permissioned list.</span></span> <span data-ttu-id="4f8bc-123">Once a proposed change reaches a majority vote by consortium members, the change is enacted.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-123">Once a proposed change reaches a majority vote by consortium members, the change is enacted.</span></span> <span data-ttu-id="4f8bc-124">This allows new consensus participants to be added or compromised participants to be removed in a transparent way that encourages an honest network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-124">This allows new consensus participants to be added or compromised participants to be removed in a transparent way that encourages an honest network.</span></span>

### <a name="admin-account"></a><span data-ttu-id="4f8bc-125">Admin account</span><span class="sxs-lookup"><span data-stu-id="4f8bc-125">Admin account</span></span>

<span data-ttu-id="4f8bc-126">During the deployment of the proof-of-authority nodes, you will be asked for an Admin Ethereum address.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-126">During the deployment of the proof-of-authority nodes, you will be asked for an Admin Ethereum address.</span></span> <span data-ttu-id="4f8bc-127">You may use several different mechanisms to generate and secure this Ethereum account.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-127">You may use several different mechanisms to generate and secure this Ethereum account.</span></span> <span data-ttu-id="4f8bc-128">Once this address is added as an authority on the network, you can use this account to participate in governance.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-128">Once this address is added as an authority on the network, you can use this account to participate in governance.</span></span> <span data-ttu-id="4f8bc-129">This admin account will also be used to delegate consensus participation to the validator nodes that are created as part of this deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-129">This admin account will also be used to delegate consensus participation to the validator nodes that are created as part of this deployment.</span></span> <span data-ttu-id="4f8bc-130">Since only the public Ethereum address is used, each admin has the flexibility to secure their private keys in a way that complies with their desired security model.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-130">Since only the public Ethereum address is used, each admin has the flexibility to secure their private keys in a way that complies with their desired security model.</span></span>

### <a name="validator-node"></a><span data-ttu-id="4f8bc-131">Validator node</span><span class="sxs-lookup"><span data-stu-id="4f8bc-131">Validator node</span></span>

<span data-ttu-id="4f8bc-132">In the proof-of-authority protocol, validator nodes take the place of traditional miner nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-132">In the proof-of-authority protocol, validator nodes take the place of traditional miner nodes.</span></span> <span data-ttu-id="4f8bc-133">Each validator has a unique Ethereum identity that gets added to a smart-contract permission list.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-133">Each validator has a unique Ethereum identity that gets added to a smart-contract permission list.</span></span> <span data-ttu-id="4f8bc-134">Once a validator is on this list, it can participate in the block creation process.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-134">Once a validator is on this list, it can participate in the block creation process.</span></span> <span data-ttu-id="4f8bc-135">To learn more about this process, see Parity's documentation on [Authority Round consensus](https://wiki.parity.io/Aura).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-135">To learn more about this process, see Parity's documentation on [Authority Round consensus](https://wiki.parity.io/Aura).</span></span> <span data-ttu-id="4f8bc-136">Each consortium member can provision two or more validator nodes across five regions, for geo-redundancy.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-136">Each consortium member can provision two or more validator nodes across five regions, for geo-redundancy.</span></span> <span data-ttu-id="4f8bc-137">Validator nodes communicate with other validator nodes to come to consensus on the state of the underlying distributed ledger.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-137">Validator nodes communicate with other validator nodes to come to consensus on the state of the underlying distributed ledger.</span></span>
<span data-ttu-id="4f8bc-138">To ensure fair participation on the network, each consortium member is prohibited from using more validators than the first member on the network (if the first member deploys three validators, each member can only have up to three validators).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-138">To ensure fair participation on the network, each consortium member is prohibited from using more validators than the first member on the network (if the first member deploys three validators, each member can only have up to three validators).</span></span>

### <a name="identity-store"></a><span data-ttu-id="4f8bc-139">Identity store</span><span class="sxs-lookup"><span data-stu-id="4f8bc-139">Identity store</span></span>

<span data-ttu-id="4f8bc-140">Since each member will have multiple validator nodes running simultaneously and each node must have a permissioned identity, it's important that the validators can safely acquire a unique active identity on the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-140">Since each member will have multiple validator nodes running simultaneously and each node must have a permissioned identity, it's important that the validators can safely acquire a unique active identity on the network.</span></span> <span data-ttu-id="4f8bc-141">To facilitate this, we've built an Identity Store that gets deployed in each member's subscription which securely holds the generated Ethereum identities.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-141">To facilitate this, we've built an Identity Store that gets deployed in each member's subscription which securely holds the generated Ethereum identities.</span></span> <span data-ttu-id="4f8bc-142">Upon deployment the orchestration container will generate an Ethereum private key for each validator and store it in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-142">Upon deployment the orchestration container will generate an Ethereum private key for each validator and store it in Azure Key Vault.</span></span> <span data-ttu-id="4f8bc-143">Before the parity node starts up, it first acquires a lease on an unused identity to ensure the identity isn't picked up by another node.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-143">Before the parity node starts up, it first acquires a lease on an unused identity to ensure the identity isn't picked up by another node.</span></span> <span data-ttu-id="4f8bc-144">The identity is provided to the client which gives it the authority to start creating blocks.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-144">The identity is provided to the client which gives it the authority to start creating blocks.</span></span> <span data-ttu-id="4f8bc-145">If the hosting VM experiences an outage, the identity lease will be released, allowing a replacement node to resume its identity in the future.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-145">If the hosting VM experiences an outage, the identity lease will be released, allowing a replacement node to resume its identity in the future.</span></span>

### <a name="bootnode-registrar"></a><span data-ttu-id="4f8bc-146">Bootnode registrar</span><span class="sxs-lookup"><span data-stu-id="4f8bc-146">Bootnode registrar</span></span>

<span data-ttu-id="4f8bc-147">To enable the ease of connectivity, each member will host a set of connection information at the [data API endpoint](#data-api).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-147">To enable the ease of connectivity, each member will host a set of connection information at the [data API endpoint](#data-api).</span></span> <span data-ttu-id="4f8bc-148">This data includes a list of bootnodes which are provided as peering nodes for the joining member.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-148">This data includes a list of bootnodes which are provided as peering nodes for the joining member.</span></span> <span data-ttu-id="4f8bc-149">As part of this data API, we keep this bootnode list up-to-date</span><span class="sxs-lookup"><span data-stu-id="4f8bc-149">As part of this data API, we keep this bootnode list up-to-date</span></span>

### <a name="bring-your-own-operator"></a><span data-ttu-id="4f8bc-150">Bring your own operator</span><span class="sxs-lookup"><span data-stu-id="4f8bc-150">Bring your own operator</span></span>

<span data-ttu-id="4f8bc-151">Often a consortium member will want to participate in network governance but don't want to operate and maintain their infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-151">Often a consortium member will want to participate in network governance but don't want to operate and maintain their infrastructure.</span></span> <span data-ttu-id="4f8bc-152">Unlike traditional systems, having a single operator across the network works against the decentralized model of blockchain systems.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-152">Unlike traditional systems, having a single operator across the network works against the decentralized model of blockchain systems.</span></span> <span data-ttu-id="4f8bc-153">Instead of hiring a centralized intermediary to operate a network, each consortium member can delegate infrastructure management to the operator of their choosing.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-153">Instead of hiring a centralized intermediary to operate a network, each consortium member can delegate infrastructure management to the operator of their choosing.</span></span> <span data-ttu-id="4f8bc-154">This allows a hybrid model where each member can choose to operate his or her own infrastructure or delegate operation to a different partner.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-154">This allows a hybrid model where each member can choose to operate his or her own infrastructure or delegate operation to a different partner.</span></span> <span data-ttu-id="4f8bc-155">The delegated operation workflow works as follows:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-155">The delegated operation workflow works as follows:</span></span>

1.  <span data-ttu-id="4f8bc-156">**Consortium Member** generates an Ethereum address (holds private key)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-156">**Consortium Member** generates an Ethereum address (holds private key)</span></span>

2.  <span data-ttu-id="4f8bc-157">**Consortium Member** provides public Ethereum address to **Operator**</span><span class="sxs-lookup"><span data-stu-id="4f8bc-157">**Consortium Member** provides public Ethereum address to **Operator**</span></span>

3.  <span data-ttu-id="4f8bc-158">**Operator** deploys and configures the PoA validator nodes using our Azure Resource Manager solution</span><span class="sxs-lookup"><span data-stu-id="4f8bc-158">**Operator** deploys and configures the PoA validator nodes using our Azure Resource Manager solution</span></span>

4.  <span data-ttu-id="4f8bc-159">**Operator** provides the RPC and management endpoint to **Consortium Member**</span><span class="sxs-lookup"><span data-stu-id="4f8bc-159">**Operator** provides the RPC and management endpoint to **Consortium Member**</span></span>

5.  <span data-ttu-id="4f8bc-160">**Consortium Member** uses their private key to sign a request accepting the validator nodes **Operator** has deployed to participate on their behalf</span><span class="sxs-lookup"><span data-stu-id="4f8bc-160">**Consortium Member** uses their private key to sign a request accepting the validator nodes **Operator** has deployed to participate on their behalf</span></span>

![Bring your own operator](./media/ethereum-poa-deployment-guide/bring-you-own-operator.png)

### <a name="azure-monitor"></a><span data-ttu-id="4f8bc-162">Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4f8bc-162">Azure Monitor</span></span>

<span data-ttu-id="4f8bc-163">This solution also comes with Azure Monitor to track node and network statistics.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-163">This solution also comes with Azure Monitor to track node and network statistics.</span></span> <span data-ttu-id="4f8bc-164">For application developers, this provides visibility into the underlying blockchain to track block generation statistics.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-164">For application developers, this provides visibility into the underlying blockchain to track block generation statistics.</span></span> <span data-ttu-id="4f8bc-165">Network operators can use Azure Monitor to quickly detect and prevent network outages through infrastructure statistics and queryable logs.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-165">Network operators can use Azure Monitor to quickly detect and prevent network outages through infrastructure statistics and queryable logs.</span></span> <span data-ttu-id="4f8bc-166">See [Service monitoring](#service-monitoring) for more details.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-166">See [Service monitoring](#service-monitoring) for more details.</span></span>

### <a name="deployment-architecture"></a><span data-ttu-id="4f8bc-167">Deployment architecture</span><span class="sxs-lookup"><span data-stu-id="4f8bc-167">Deployment architecture</span></span>

#### <a name="description"></a><span data-ttu-id="4f8bc-168">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-168">Description</span></span>

<span data-ttu-id="4f8bc-169">This solution can deploy a single or multi-region based multi-member Ethereum consortium network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-169">This solution can deploy a single or multi-region based multi-member Ethereum consortium network.</span></span> <span data-ttu-id="4f8bc-170">By default, the RPC and peering endpoints are accessible over public IP to enable simplified connectivity across subscriptions and clouds.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-170">By default, the RPC and peering endpoints are accessible over public IP to enable simplified connectivity across subscriptions and clouds.</span></span> <span data-ttu-id="4f8bc-171">We recommend leveraging [Parity's permissioning contracts](https://wiki.parity.io/Permissioning) for application level access-controls.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-171">We recommend leveraging [Parity's permissioning contracts](https://wiki.parity.io/Permissioning) for application level access-controls.</span></span> <span data-ttu-id="4f8bc-172">We also support networks deployed behind VPNs, which leverage VNet gateways for cross-subscription connectivity.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-172">We also support networks deployed behind VPNs, which leverage VNet gateways for cross-subscription connectivity.</span></span> <span data-ttu-id="4f8bc-173">These deployments are more complex, so it is recommended to start with the public IP model first.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-173">These deployments are more complex, so it is recommended to start with the public IP model first.</span></span>

#### <a name="consortium-member-overview"></a><span data-ttu-id="4f8bc-174">Consortium member overview</span><span class="sxs-lookup"><span data-stu-id="4f8bc-174">Consortium member overview</span></span>

<span data-ttu-id="4f8bc-175">Each consortium member deployment includes:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-175">Each consortium member deployment includes:</span></span>

-   <span data-ttu-id="4f8bc-176">Virtual M Scale Sets (VMSS) for running the PoA validators</span><span class="sxs-lookup"><span data-stu-id="4f8bc-176">Virtual M Scale Sets (VMSS) for running the PoA validators</span></span>

-   <span data-ttu-id="4f8bc-177">Azure Load Balancer for distributing RPC, peering, and Governance DApp requests</span><span class="sxs-lookup"><span data-stu-id="4f8bc-177">Azure Load Balancer for distributing RPC, peering, and Governance DApp requests</span></span>

-   <span data-ttu-id="4f8bc-178">Azure Key Vault for securing the validator identities</span><span class="sxs-lookup"><span data-stu-id="4f8bc-178">Azure Key Vault for securing the validator identities</span></span>

-   <span data-ttu-id="4f8bc-179">Azure Storage for hosting persistent network information and coordinating leasing</span><span class="sxs-lookup"><span data-stu-id="4f8bc-179">Azure Storage for hosting persistent network information and coordinating leasing</span></span>

-   <span data-ttu-id="4f8bc-180">Azure Monitor for aggregating logs and performance statistics</span><span class="sxs-lookup"><span data-stu-id="4f8bc-180">Azure Monitor for aggregating logs and performance statistics</span></span>

-   <span data-ttu-id="4f8bc-181">VNet Gateway (optional) for allowing VPN connections across private VNets</span><span class="sxs-lookup"><span data-stu-id="4f8bc-181">VNet Gateway (optional) for allowing VPN connections across private VNets</span></span>

![deployment architecture](./media/ethereum-poa-deployment-guide/deployment-architecture.png)

<span data-ttu-id="4f8bc-183">We leverage Docker containers for reliability and modularity.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-183">We leverage Docker containers for reliability and modularity.</span></span> <span data-ttu-id="4f8bc-184">We use Azure Container Registry to host and serve versioned images as part of each deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-184">We use Azure Container Registry to host and serve versioned images as part of each deployment.</span></span> <span data-ttu-id="4f8bc-185">The container images consist of:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-185">The container images consist of:</span></span>

-   <span data-ttu-id="4f8bc-186">Orchestrator</span><span class="sxs-lookup"><span data-stu-id="4f8bc-186">Orchestrator</span></span>

    -   <span data-ttu-id="4f8bc-187">Runs once during deployment</span><span class="sxs-lookup"><span data-stu-id="4f8bc-187">Runs once during deployment</span></span>

    -   <span data-ttu-id="4f8bc-188">Generates identities and governance contracts</span><span class="sxs-lookup"><span data-stu-id="4f8bc-188">Generates identities and governance contracts</span></span>

    -   <span data-ttu-id="4f8bc-189">Stores identities in Identity Store</span><span class="sxs-lookup"><span data-stu-id="4f8bc-189">Stores identities in Identity Store</span></span>

-   <span data-ttu-id="4f8bc-190">Parity Client</span><span class="sxs-lookup"><span data-stu-id="4f8bc-190">Parity Client</span></span>

    -   <span data-ttu-id="4f8bc-191">Leases identity from Identity Store</span><span class="sxs-lookup"><span data-stu-id="4f8bc-191">Leases identity from Identity Store</span></span>

    -   <span data-ttu-id="4f8bc-192">Discovers and connects to peers</span><span class="sxs-lookup"><span data-stu-id="4f8bc-192">Discovers and connects to peers</span></span>

-   <span data-ttu-id="4f8bc-193">EthStats Agent</span><span class="sxs-lookup"><span data-stu-id="4f8bc-193">EthStats Agent</span></span>

    -   <span data-ttu-id="4f8bc-194">Collects local logs and stats via RPC and pushes to Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4f8bc-194">Collects local logs and stats via RPC and pushes to Azure Monitor</span></span>

-   <span data-ttu-id="4f8bc-195">Governance DApp</span><span class="sxs-lookup"><span data-stu-id="4f8bc-195">Governance DApp</span></span>

    -   <span data-ttu-id="4f8bc-196">Web interface for interacting with Governance contracts</span><span class="sxs-lookup"><span data-stu-id="4f8bc-196">Web interface for interacting with Governance contracts</span></span>

## <a name="governance-dapp"></a><span data-ttu-id="4f8bc-197">Governance DApp</span><span class="sxs-lookup"><span data-stu-id="4f8bc-197">Governance DApp</span></span>

<span data-ttu-id="4f8bc-198">At the heart of proof-of-authority is decentralized governance.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-198">At the heart of proof-of-authority is decentralized governance.</span></span> <span data-ttu-id="4f8bc-199">The governance DApp is a set of pre-deployed smart contracts and a web application that are used to govern the authorities on the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-199">The governance DApp is a set of pre-deployed smart contracts and a web application that are used to govern the authorities on the network.</span></span>
<span data-ttu-id="4f8bc-200">Authorities are broken up into Admin identities and Validator nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-200">Authorities are broken up into Admin identities and Validator nodes.</span></span>
<span data-ttu-id="4f8bc-201">Admins have the power to delegate consensus participation to a set of Validator nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-201">Admins have the power to delegate consensus participation to a set of Validator nodes.</span></span> <span data-ttu-id="4f8bc-202">Admins also may vote other admins into or out of the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-202">Admins also may vote other admins into or out of the network.</span></span>

![governance dapp](./media/ethereum-poa-deployment-guide/governance-dapp.png)

-   <span data-ttu-id="4f8bc-204">**Decentralized Governance -** Changes in network authorities are administered through on-chain voting by select administrators.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-204">**Decentralized Governance -** Changes in network authorities are administered through on-chain voting by select administrators.</span></span>

-   <span data-ttu-id="4f8bc-205">**Validator Delegation -** Authorities can manage their validator nodes that are set up in each PoA deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-205">**Validator Delegation -** Authorities can manage their validator nodes that are set up in each PoA deployment.</span></span>

-   <span data-ttu-id="4f8bc-206">**Auditable Change History -** Each change is recorded on the blockchain providing transparency and auditability.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-206">**Auditable Change History -** Each change is recorded on the blockchain providing transparency and auditability.</span></span>

## <a name="how-to-guides"></a><span data-ttu-id="4f8bc-207">How-to guides</span><span class="sxs-lookup"><span data-stu-id="4f8bc-207">How-to guides</span></span>

### <a name="deploy-ethereum-proof-of-authority"></a><span data-ttu-id="4f8bc-208">Deploy Ethereum Proof-of-Authority</span><span class="sxs-lookup"><span data-stu-id="4f8bc-208">Deploy Ethereum Proof-of-Authority</span></span>

<span data-ttu-id="4f8bc-209">Here's an example of a multi-party deployment flow:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-209">Here's an example of a multi-party deployment flow:</span></span>

1.  <span data-ttu-id="4f8bc-210">Three members each generate an Ethereum account using MetaMask</span><span class="sxs-lookup"><span data-stu-id="4f8bc-210">Three members each generate an Ethereum account using MetaMask</span></span>

2.  <span data-ttu-id="4f8bc-211">*Member A* deploys Ethereum PoA, providing their Ethereum Public Address</span><span class="sxs-lookup"><span data-stu-id="4f8bc-211">*Member A* deploys Ethereum PoA, providing their Ethereum Public Address</span></span>

3.  <span data-ttu-id="4f8bc-212">*Member A* provides the consortium URL to *Member B* and *Member C*</span><span class="sxs-lookup"><span data-stu-id="4f8bc-212">*Member A* provides the consortium URL to *Member B* and *Member C*</span></span>

4.  <span data-ttu-id="4f8bc-213">*Member B* and *Member C* deploy, Ethereum PoA, providing their Ethereum Public Address and *Member A*'s consortium URL</span><span class="sxs-lookup"><span data-stu-id="4f8bc-213">*Member B* and *Member C* deploy, Ethereum PoA, providing their Ethereum Public Address and *Member A*'s consortium URL</span></span>

5.  <span data-ttu-id="4f8bc-214">*Member A* votes in *Member B* as an admin</span><span class="sxs-lookup"><span data-stu-id="4f8bc-214">*Member A* votes in *Member B* as an admin</span></span>

6.  <span data-ttu-id="4f8bc-215">*Member A* and *Member B* both vote *Member C* as an admin</span><span class="sxs-lookup"><span data-stu-id="4f8bc-215">*Member A* and *Member B* both vote *Member C* as an admin</span></span>

<span data-ttu-id="4f8bc-216">This process requires an Azure subscription that can support deploying several virtual machines scale sets and managed disks.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-216">This process requires an Azure subscription that can support deploying several virtual machines scale sets and managed disks.</span></span> <span data-ttu-id="4f8bc-217">If necessary, [create a free Azure account](https://azure.microsoft.com/free/) to begin.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-217">If necessary, [create a free Azure account](https://azure.microsoft.com/free/) to begin.</span></span>

<span data-ttu-id="4f8bc-218">Once a subscription is secured, go to Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-218">Once a subscription is secured, go to Azure portal.</span></span> <span data-ttu-id="4f8bc-219">Select '+', Marketplace ('See all'), and search for Ethereum PoA Consortium.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-219">Select '+', Marketplace ('See all'), and search for Ethereum PoA Consortium.</span></span>

<span data-ttu-id="4f8bc-220">The following section will walk you through configuring the first member's footprint in the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-220">The following section will walk you through configuring the first member's footprint in the network.</span></span> <span data-ttu-id="4f8bc-221">The deployment flow is divided into five steps: Basics, Deployment regions, Network size and performance, Ethereum settings, Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-221">The deployment flow is divided into five steps: Basics, Deployment regions, Network size and performance, Ethereum settings, Azure Monitor.</span></span>

#### <a name="basics"></a><span data-ttu-id="4f8bc-222">Basics</span><span class="sxs-lookup"><span data-stu-id="4f8bc-222">Basics</span></span>

<span data-ttu-id="4f8bc-223">Under **Basics**, specify values for standard parameters for any deployment, such as subscription, resource group and basic virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-223">Under **Basics**, specify values for standard parameters for any deployment, such as subscription, resource group and basic virtual machine properties.</span></span>

<span data-ttu-id="4f8bc-224">A detailed description of each parameter follows:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-224">A detailed description of each parameter follows:</span></span>

<span data-ttu-id="4f8bc-225">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-225">Parameter Name</span></span>|<span data-ttu-id="4f8bc-226">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-226">Description</span></span>|<span data-ttu-id="4f8bc-227">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-227">Allowed Values</span></span>|<span data-ttu-id="4f8bc-228">Default Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-228">Default Values</span></span>    
---|---|---|---
<span data-ttu-id="4f8bc-229">Create a new network or join existing network?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-229">Create a new network or join existing network?</span></span>|<span data-ttu-id="4f8bc-230">Create a new network or join a preexisting consortium network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-230">Create a new network or join a preexisting consortium network</span></span>|<span data-ttu-id="4f8bc-231">Create New Join Existing</span><span class="sxs-lookup"><span data-stu-id="4f8bc-231">Create New Join Existing</span></span>|<span data-ttu-id="4f8bc-232">Create New</span><span class="sxs-lookup"><span data-stu-id="4f8bc-232">Create New</span></span>
<span data-ttu-id="4f8bc-233">Email Address (Optional)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-233">Email Address (Optional)</span></span>|<span data-ttu-id="4f8bc-234">You'll receive an email notification when your deployment completes with information about your deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-234">You'll receive an email notification when your deployment completes with information about your deployment.</span></span>|<span data-ttu-id="4f8bc-235">Valid email address</span><span class="sxs-lookup"><span data-stu-id="4f8bc-235">Valid email address</span></span>|<span data-ttu-id="4f8bc-236">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-236">NA</span></span>
<span data-ttu-id="4f8bc-237">VM user name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-237">VM user name</span></span>|<span data-ttu-id="4f8bc-238">Administrator username of each deployed VM (alphanumeric characters only)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-238">Administrator username of each deployed VM (alphanumeric characters only)</span></span>|<span data-ttu-id="4f8bc-239">1-64 characters</span><span class="sxs-lookup"><span data-stu-id="4f8bc-239">1-64 characters</span></span>|<span data-ttu-id="4f8bc-240">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-240">NA</span></span>
<span data-ttu-id="4f8bc-241">Authentication type</span><span class="sxs-lookup"><span data-stu-id="4f8bc-241">Authentication type</span></span>|<span data-ttu-id="4f8bc-242">The method to authenticate to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-242">The method to authenticate to the virtual machine.</span></span>|<span data-ttu-id="4f8bc-243">Password or SSH public key</span><span class="sxs-lookup"><span data-stu-id="4f8bc-243">Password or SSH public key</span></span>|<span data-ttu-id="4f8bc-244">Password</span><span class="sxs-lookup"><span data-stu-id="4f8bc-244">Password</span></span>
<span data-ttu-id="4f8bc-245">Password (Authentication type = Password)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-245">Password (Authentication type = Password)</span></span>|<span data-ttu-id="4f8bc-246">The password for the administrator account for each of the virtual machines deployed.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-246">The password for the administrator account for each of the virtual machines deployed.</span></span>  <span data-ttu-id="4f8bc-247">The password must contain 3 of the following: 1 upper case character, 1 lower case character, 1 number, and 1 special character.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-247">The password must contain 3 of the following: 1 upper case character, 1 lower case character, 1 number, and 1 special character.</span></span> <span data-ttu-id="4f8bc-248">While all VMs initially have the same password, you can change the password after provisioning.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-248">While all VMs initially have the same password, you can change the password after provisioning.</span></span>|<span data-ttu-id="4f8bc-249">12-72 characters</span><span class="sxs-lookup"><span data-stu-id="4f8bc-249">12-72 characters</span></span>|<span data-ttu-id="4f8bc-250">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-250">NA</span></span>
<span data-ttu-id="4f8bc-251">SSH Key (Authentication type = Public Key)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-251">SSH Key (Authentication type = Public Key)</span></span>|<span data-ttu-id="4f8bc-252">The secure shell key used for remote login.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-252">The secure shell key used for remote login.</span></span>||<span data-ttu-id="4f8bc-253">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-253">NA</span></span>
<span data-ttu-id="4f8bc-254">Subscription</span><span class="sxs-lookup"><span data-stu-id="4f8bc-254">Subscription</span></span>|<span data-ttu-id="4f8bc-255">The subscription to which to deploy the consortium network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-255">The subscription to which to deploy the consortium network</span></span>||<span data-ttu-id="4f8bc-256">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-256">NA</span></span>
<span data-ttu-id="4f8bc-257">Resource Group</span><span class="sxs-lookup"><span data-stu-id="4f8bc-257">Resource Group</span></span>|<span data-ttu-id="4f8bc-258">The resource group to which to deploy the consortium network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-258">The resource group to which to deploy the consortium network.</span></span>||<span data-ttu-id="4f8bc-259">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-259">NA</span></span>
<span data-ttu-id="4f8bc-260">Location</span><span class="sxs-lookup"><span data-stu-id="4f8bc-260">Location</span></span>|<span data-ttu-id="4f8bc-261">The Azure region for resource group.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-261">The Azure region for resource group.</span></span>||<span data-ttu-id="4f8bc-262">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-262">NA</span></span>

<span data-ttu-id="4f8bc-263">A sample deployment is shown below: ![basic blade](./media/ethereum-poa-deployment-guide/basic-blade.png)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-263">A sample deployment is shown below: ![basic blade](./media/ethereum-poa-deployment-guide/basic-blade.png)</span></span>

#### <a name="deployment-regions"></a><span data-ttu-id="4f8bc-264">Deployment regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-264">Deployment regions</span></span>

<span data-ttu-id="4f8bc-265">Next, under Deployment regions, specify inputs for number of region(s) to deploy the consortium network and selection of Azure regions based on the number of regions given.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-265">Next, under Deployment regions, specify inputs for number of region(s) to deploy the consortium network and selection of Azure regions based on the number of regions given.</span></span> <span data-ttu-id="4f8bc-266">User can deploy in maximum of 5 regions.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-266">User can deploy in maximum of 5 regions.</span></span> <span data-ttu-id="4f8bc-267">We recommend choosing the first region to match the resource group location from Basics section.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-267">We recommend choosing the first region to match the resource group location from Basics section.</span></span> <span data-ttu-id="4f8bc-268">For development or test networks, a single region per member is recommended.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-268">For development or test networks, a single region per member is recommended.</span></span> <span data-ttu-id="4f8bc-269">For production, we recommend deploying across two or more regions for high-availability.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-269">For production, we recommend deploying across two or more regions for high-availability.</span></span>

<span data-ttu-id="4f8bc-270">A detailed description of each parameter follows:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-270">A detailed description of each parameter follows:</span></span>

  <span data-ttu-id="4f8bc-271">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-271">Parameter Name</span></span>|<span data-ttu-id="4f8bc-272">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-272">Description</span></span>|<span data-ttu-id="4f8bc-273">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-273">Allowed Values</span></span>|<span data-ttu-id="4f8bc-274">Default Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-274">Default Values</span></span>
  ---|---|---|---
  <span data-ttu-id="4f8bc-275">Number of region(s)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-275">Number of region(s)</span></span>|<span data-ttu-id="4f8bc-276">Number of regions to deploy the consortium network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-276">Number of regions to deploy the consortium network</span></span>|<span data-ttu-id="4f8bc-277">1, 2, 3, 4, 5</span><span class="sxs-lookup"><span data-stu-id="4f8bc-277">1, 2, 3, 4, 5</span></span>|<span data-ttu-id="4f8bc-278">1</span><span class="sxs-lookup"><span data-stu-id="4f8bc-278">1</span></span>
  <span data-ttu-id="4f8bc-279">First region</span><span class="sxs-lookup"><span data-stu-id="4f8bc-279">First region</span></span>|<span data-ttu-id="4f8bc-280">First region to deploy the consortium network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-280">First region to deploy the consortium network</span></span>|<span data-ttu-id="4f8bc-281">All allowed Azure regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-281">All allowed Azure regions</span></span>|<span data-ttu-id="4f8bc-282">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-282">NA</span></span>
  <span data-ttu-id="4f8bc-283">Second region</span><span class="sxs-lookup"><span data-stu-id="4f8bc-283">Second region</span></span>|<span data-ttu-id="4f8bc-284">Second region to deploy the consortium network (Visible only when number of regions is selected as 2)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-284">Second region to deploy the consortium network (Visible only when number of regions is selected as 2)</span></span>|<span data-ttu-id="4f8bc-285">All allowed Azure regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-285">All allowed Azure regions</span></span>|<span data-ttu-id="4f8bc-286">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-286">NA</span></span>
  <span data-ttu-id="4f8bc-287">Third region</span><span class="sxs-lookup"><span data-stu-id="4f8bc-287">Third region</span></span>|<span data-ttu-id="4f8bc-288">Third region to deploy the consortium network (Visible only when number of regions is selected as 3)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-288">Third region to deploy the consortium network (Visible only when number of regions is selected as 3)</span></span>|<span data-ttu-id="4f8bc-289">All allowed Azure regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-289">All allowed Azure regions</span></span>|<span data-ttu-id="4f8bc-290">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-290">NA</span></span>
  <span data-ttu-id="4f8bc-291">Fourth region</span><span class="sxs-lookup"><span data-stu-id="4f8bc-291">Fourth region</span></span>|<span data-ttu-id="4f8bc-292">Fourth region to deploy the consortium network (Visible only when number of regions is selected as 4)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-292">Fourth region to deploy the consortium network (Visible only when number of regions is selected as 4)</span></span>|<span data-ttu-id="4f8bc-293">All allowed Azure regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-293">All allowed Azure regions</span></span>|<span data-ttu-id="4f8bc-294">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-294">NA</span></span>
  <span data-ttu-id="4f8bc-295">Fifth region</span><span class="sxs-lookup"><span data-stu-id="4f8bc-295">Fifth region</span></span>|<span data-ttu-id="4f8bc-296">Fifth region to deploy the consortium network (Visible only when number of regions is selected as 5)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-296">Fifth region to deploy the consortium network (Visible only when number of regions is selected as 5)</span></span>|<span data-ttu-id="4f8bc-297">All allowed Azure regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-297">All allowed Azure regions</span></span>|<span data-ttu-id="4f8bc-298">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-298">NA</span></span>

<span data-ttu-id="4f8bc-299">A sample deployment is shown below: ![deployment regions](./media/ethereum-poa-deployment-guide/deployment-regions.png)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-299">A sample deployment is shown below: ![deployment regions](./media/ethereum-poa-deployment-guide/deployment-regions.png)</span></span>

#### <a name="network-size-and-performance"></a><span data-ttu-id="4f8bc-300">Network size and performance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-300">Network size and performance</span></span> 

<span data-ttu-id="4f8bc-301">Next, under 'Network size and performance' specify inputs for the size of the consortium network, such as number and size of validator nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-301">Next, under 'Network size and performance' specify inputs for the size of the consortium network, such as number and size of validator nodes.</span></span>
<span data-ttu-id="4f8bc-302">The validator node storage size will dictate the potential size of the blockchain.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-302">The validator node storage size will dictate the potential size of the blockchain.</span></span> <span data-ttu-id="4f8bc-303">This can be changed after deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-303">This can be changed after deployment.</span></span>

<span data-ttu-id="4f8bc-304">A detailed description of each parameter follows:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-304">A detailed description of each parameter follows:</span></span>

  <span data-ttu-id="4f8bc-305">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-305">Parameter Name</span></span>|<span data-ttu-id="4f8bc-306">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-306">Description</span></span>|<span data-ttu-id="4f8bc-307">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-307">Allowed Values</span></span>|<span data-ttu-id="4f8bc-308">Default Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-308">Default Values</span></span>
  ---|---|---|---
  <span data-ttu-id="4f8bc-309">Number of load balanced validator nodes</span><span class="sxs-lookup"><span data-stu-id="4f8bc-309">Number of load balanced validator nodes</span></span>|<span data-ttu-id="4f8bc-310">The number of validator nodes to provision as part of the network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-310">The number of validator nodes to provision as part of the network</span></span>|<span data-ttu-id="4f8bc-311">2-15</span><span class="sxs-lookup"><span data-stu-id="4f8bc-311">2-15</span></span>|<span data-ttu-id="4f8bc-312">2</span><span class="sxs-lookup"><span data-stu-id="4f8bc-312">2</span></span>
  <span data-ttu-id="4f8bc-313">Validator node storage performance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-313">Validator node storage performance</span></span>|<span data-ttu-id="4f8bc-314">The type of managed disk backing each of the deployed validator nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-314">The type of managed disk backing each of the deployed validator nodes.</span></span>|<span data-ttu-id="4f8bc-315">Standard or Premium</span><span class="sxs-lookup"><span data-stu-id="4f8bc-315">Standard or Premium</span></span>|<span data-ttu-id="4f8bc-316">Standard</span><span class="sxs-lookup"><span data-stu-id="4f8bc-316">Standard</span></span>
  <span data-ttu-id="4f8bc-317">Validator node virtual machine size</span><span class="sxs-lookup"><span data-stu-id="4f8bc-317">Validator node virtual machine size</span></span>|<span data-ttu-id="4f8bc-318">The virtual machine size used for validator nodes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-318">The virtual machine size used for validator nodes.</span></span>|<span data-ttu-id="4f8bc-319">Standard A, Standard D, Standard D-v2, Standard F series, Standard DS, and Standard FS</span><span class="sxs-lookup"><span data-stu-id="4f8bc-319">Standard A, Standard D, Standard D-v2, Standard F series, Standard DS, and Standard FS</span></span>|<span data-ttu-id="4f8bc-320">Standard D1 v2</span><span class="sxs-lookup"><span data-stu-id="4f8bc-320">Standard D1 v2</span></span>

<span data-ttu-id="4f8bc-321">A sample deployment is shown below: ![network size and performance](./media/ethereum-poa-deployment-guide/network-size-and-performance.png)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-321">A sample deployment is shown below: ![network size and performance](./media/ethereum-poa-deployment-guide/network-size-and-performance.png)</span></span>

#### <a name="ethereum-settings"></a><span data-ttu-id="4f8bc-322">Ethereum Settings</span><span class="sxs-lookup"><span data-stu-id="4f8bc-322">Ethereum Settings</span></span>

<span data-ttu-id="4f8bc-323">Next, under Ethereum settings, specify Ethereum-related configuration settings, like the network ID and Ethereum account password or genesis block.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-323">Next, under Ethereum settings, specify Ethereum-related configuration settings, like the network ID and Ethereum account password or genesis block.</span></span>

<span data-ttu-id="4f8bc-324">A detailed description of each parameter follows:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-324">A detailed description of each parameter follows:</span></span>

  <span data-ttu-id="4f8bc-325">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-325">Parameter Name</span></span>|<span data-ttu-id="4f8bc-326">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-326">Description</span></span>|<span data-ttu-id="4f8bc-327">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-327">Allowed Values</span></span>|<span data-ttu-id="4f8bc-328">Default Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-328">Default Values</span></span>
  ---|---|---|---
<span data-ttu-id="4f8bc-329">Consortium Member ID</span><span class="sxs-lookup"><span data-stu-id="4f8bc-329">Consortium Member ID</span></span>|<span data-ttu-id="4f8bc-330">The ID associated with each member participating in the consortium network used to configure IP address spaces to avoid collision.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-330">The ID associated with each member participating in the consortium network used to configure IP address spaces to avoid collision.</span></span> <span data-ttu-id="4f8bc-331">In the case of a private network, Member ID should be unique across different organizations in the same network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-331">In the case of a private network, Member ID should be unique across different organizations in the same network.</span></span>  <span data-ttu-id="4f8bc-332">A unique member ID is needed even when the same organization deploys to multiple regions.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-332">A unique member ID is needed even when the same organization deploys to multiple regions.</span></span> <span data-ttu-id="4f8bc-333">Make note of the value of this parameter since you will need to share it with other joining members to ensure there’s no collision.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-333">Make note of the value of this parameter since you will need to share it with other joining members to ensure there’s no collision.</span></span>|<span data-ttu-id="4f8bc-334">0-255</span><span class="sxs-lookup"><span data-stu-id="4f8bc-334">0-255</span></span>|<span data-ttu-id="4f8bc-335">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-335">NA</span></span>
<span data-ttu-id="4f8bc-336">Network ID</span><span class="sxs-lookup"><span data-stu-id="4f8bc-336">Network ID</span></span>|<span data-ttu-id="4f8bc-337">The network ID for the consortium Ethereum network being deployed.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-337">The network ID for the consortium Ethereum network being deployed.</span></span>  <span data-ttu-id="4f8bc-338">Each Ethereum network has its own Network ID, with 1 being the ID for the public network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-338">Each Ethereum network has its own Network ID, with 1 being the ID for the public network.</span></span>|<span data-ttu-id="4f8bc-339">5 - 999,999,999</span><span class="sxs-lookup"><span data-stu-id="4f8bc-339">5 - 999,999,999</span></span>|<span data-ttu-id="4f8bc-340">10101010</span><span class="sxs-lookup"><span data-stu-id="4f8bc-340">10101010</span></span>
<span data-ttu-id="4f8bc-341">Admin Ethereum Address</span><span class="sxs-lookup"><span data-stu-id="4f8bc-341">Admin Ethereum Address</span></span>|<span data-ttu-id="4f8bc-342">Ethereum account address that is used for participating in PoA governance.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-342">Ethereum account address that is used for participating in PoA governance.</span></span>  <span data-ttu-id="4f8bc-343">We recommend using MetaMask for generating an Ethereum address.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-343">We recommend using MetaMask for generating an Ethereum address.</span></span>|<span data-ttu-id="4f8bc-344">42 alphanumeric characters starting with 0x</span><span class="sxs-lookup"><span data-stu-id="4f8bc-344">42 alphanumeric characters starting with 0x</span></span>|<span data-ttu-id="4f8bc-345">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-345">NA</span></span>
<span data-ttu-id="4f8bc-346">Advanced Options</span><span class="sxs-lookup"><span data-stu-id="4f8bc-346">Advanced Options</span></span>|<span data-ttu-id="4f8bc-347">Advanced options for Ethereum settings</span><span class="sxs-lookup"><span data-stu-id="4f8bc-347">Advanced options for Ethereum settings</span></span>|<span data-ttu-id="4f8bc-348">Enable or Disable</span><span class="sxs-lookup"><span data-stu-id="4f8bc-348">Enable or Disable</span></span>|<span data-ttu-id="4f8bc-349">Disable</span><span class="sxs-lookup"><span data-stu-id="4f8bc-349">Disable</span></span>
<span data-ttu-id="4f8bc-350">Public IP (Advanced Options = Enable)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-350">Public IP (Advanced Options = Enable)</span></span>|<span data-ttu-id="4f8bc-351">Deploys the network behind a VNet Gateway and removes peering access.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-351">Deploys the network behind a VNet Gateway and removes peering access.</span></span> <span data-ttu-id="4f8bc-352">If this option is selected, all members must use a VNet Gateway for the connection to be compatible.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-352">If this option is selected, all members must use a VNet Gateway for the connection to be compatible.</span></span>|<span data-ttu-id="4f8bc-353">Public IP Private VNet</span><span class="sxs-lookup"><span data-stu-id="4f8bc-353">Public IP Private VNet</span></span>|<span data-ttu-id="4f8bc-354">Public IP</span><span class="sxs-lookup"><span data-stu-id="4f8bc-354">Public IP</span></span>
<span data-ttu-id="4f8bc-355">Transaction Permission Contract (Advanced Options = Enable)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-355">Transaction Permission Contract (Advanced Options = Enable)</span></span>|<span data-ttu-id="4f8bc-356">Bytecode for the Transaction Permissioning contract.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-356">Bytecode for the Transaction Permissioning contract.</span></span> <span data-ttu-id="4f8bc-357">Restricts smart contract deployment and execution to a permissioned list of Ethereum accounts.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-357">Restricts smart contract deployment and execution to a permissioned list of Ethereum accounts.</span></span>|<span data-ttu-id="4f8bc-358">Contract bytecode</span><span class="sxs-lookup"><span data-stu-id="4f8bc-358">Contract bytecode</span></span>|<span data-ttu-id="4f8bc-359">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-359">NA</span></span>

<span data-ttu-id="4f8bc-360">A sample deployment is shown below: ![ethereum settings](./media/ethereum-poa-deployment-guide/ethereum-settings.png)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-360">A sample deployment is shown below: ![ethereum settings](./media/ethereum-poa-deployment-guide/ethereum-settings.png)</span></span>

#### <a name="azure-monitor"></a><span data-ttu-id="4f8bc-361">Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4f8bc-361">Azure Monitor</span></span>

<span data-ttu-id="4f8bc-362">The Azure Monitor blade allows you to configure an Azure Monitor resource for your network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-362">The Azure Monitor blade allows you to configure an Azure Monitor resource for your network.</span></span> <span data-ttu-id="4f8bc-363">Azure Monitor will collect and surface useful metrics and logs from your network, providing the ability to quickly check the network health or debug issues.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-363">Azure Monitor will collect and surface useful metrics and logs from your network, providing the ability to quickly check the network health or debug issues.</span></span>

  <span data-ttu-id="4f8bc-364">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="4f8bc-364">Parameter Name</span></span>|<span data-ttu-id="4f8bc-365">Description</span><span class="sxs-lookup"><span data-stu-id="4f8bc-365">Description</span></span>|<span data-ttu-id="4f8bc-366">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-366">Allowed Values</span></span>|<span data-ttu-id="4f8bc-367">Default Values</span><span class="sxs-lookup"><span data-stu-id="4f8bc-367">Default Values</span></span>
  ---|---|---|---
<span data-ttu-id="4f8bc-368">Monitoring</span><span class="sxs-lookup"><span data-stu-id="4f8bc-368">Monitoring</span></span>|<span data-ttu-id="4f8bc-369">Option to enable Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4f8bc-369">Option to enable Azure Monitor</span></span>|<span data-ttu-id="4f8bc-370">Enable or Disable</span><span class="sxs-lookup"><span data-stu-id="4f8bc-370">Enable or Disable</span></span>|<span data-ttu-id="4f8bc-371">Enable</span><span class="sxs-lookup"><span data-stu-id="4f8bc-371">Enable</span></span>
<span data-ttu-id="4f8bc-372">Connect to existing Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4f8bc-372">Connect to existing Log Analytics</span></span>|<span data-ttu-id="4f8bc-373">Create a new Log Analytics instance as part of Azure Monitor or join an existing instance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-373">Create a new Log Analytics instance as part of Azure Monitor or join an existing instance</span></span>|<span data-ttu-id="4f8bc-374">Create new or Join existing</span><span class="sxs-lookup"><span data-stu-id="4f8bc-374">Create new or Join existing</span></span>|<span data-ttu-id="4f8bc-375">Create new</span><span class="sxs-lookup"><span data-stu-id="4f8bc-375">Create new</span></span>
<span data-ttu-id="4f8bc-376">Azure Monitor Location(Connect to Existing Azure Monitor = Create new)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-376">Azure Monitor Location(Connect to Existing Azure Monitor = Create new)</span></span>|<span data-ttu-id="4f8bc-377">The region where the new Azure Monitor will be deployed</span><span class="sxs-lookup"><span data-stu-id="4f8bc-377">The region where the new Azure Monitor will be deployed</span></span>|<span data-ttu-id="4f8bc-378">All Azure Monitor  regions</span><span class="sxs-lookup"><span data-stu-id="4f8bc-378">All Azure Monitor  regions</span></span>|<span data-ttu-id="4f8bc-379">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-379">NA</span></span>
<span data-ttu-id="4f8bc-380">Existing Log Analytics Workspace Id (Connect to Existing Azure Monitor = Join Existing)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-380">Existing Log Analytics Workspace Id (Connect to Existing Azure Monitor = Join Existing)</span></span>|<span data-ttu-id="4f8bc-381">Workspace ID of the existing Log Analytics instance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-381">Workspace ID of the existing Log Analytics instance</span></span>||<span data-ttu-id="4f8bc-382">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-382">NA</span></span>
<span data-ttu-id="4f8bc-383">Existing Log Analytics Primary Key (Connect to Existing Azure Monitor = Join Existing)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-383">Existing Log Analytics Primary Key (Connect to Existing Azure Monitor = Join Existing)</span></span>|<span data-ttu-id="4f8bc-384">The primary key used to connect to the existing Azure Monitor instance</span><span class="sxs-lookup"><span data-stu-id="4f8bc-384">The primary key used to connect to the existing Azure Monitor instance</span></span>||<span data-ttu-id="4f8bc-385">NA</span><span class="sxs-lookup"><span data-stu-id="4f8bc-385">NA</span></span>


<span data-ttu-id="4f8bc-386">A sample deployment is shown below: ![azure monitor](./media/ethereum-poa-deployment-guide/azure-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-386">A sample deployment is shown below: ![azure monitor](./media/ethereum-poa-deployment-guide/azure-monitor.png)</span></span>

#### <a name="summary"></a><span data-ttu-id="4f8bc-387">Summary</span><span class="sxs-lookup"><span data-stu-id="4f8bc-387">Summary</span></span>

<span data-ttu-id="4f8bc-388">Click through the summary blade to review the inputs specified and to run basic pre-deployment validation.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-388">Click through the summary blade to review the inputs specified and to run basic pre-deployment validation.</span></span> <span data-ttu-id="4f8bc-389">Before deploying you may download the template and parameters.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-389">Before deploying you may download the template and parameters.</span></span>

<span data-ttu-id="4f8bc-390">Review legal and privacy terms and click 'Purchase' to deploy.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-390">Review legal and privacy terms and click 'Purchase' to deploy.</span></span> <span data-ttu-id="4f8bc-391">If the deployment includes VNet Gateways, the deployment will take up 45 to 50 minutes.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-391">If the deployment includes VNet Gateways, the deployment will take up 45 to 50 minutes.</span></span>

#### <a name="post-deployment"></a><span data-ttu-id="4f8bc-392">Post Deployment</span><span class="sxs-lookup"><span data-stu-id="4f8bc-392">Post Deployment</span></span>

##### <a name="deployment-output"></a><span data-ttu-id="4f8bc-393">Deployment Output</span><span class="sxs-lookup"><span data-stu-id="4f8bc-393">Deployment Output</span></span> 

<span data-ttu-id="4f8bc-394">Once the deployment has completed, you'll be able to access the necessary parameters via the confirmation email or through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-394">Once the deployment has completed, you'll be able to access the necessary parameters via the confirmation email or through the Azure portal.</span></span> <span data-ttu-id="4f8bc-395">In these parameters you'll find:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-395">In these parameters you'll find:</span></span>

-   <span data-ttu-id="4f8bc-396">Ethereum RPC endpoint</span><span class="sxs-lookup"><span data-stu-id="4f8bc-396">Ethereum RPC endpoint</span></span>

-   <span data-ttu-id="4f8bc-397">Governance Dashboard URL</span><span class="sxs-lookup"><span data-stu-id="4f8bc-397">Governance Dashboard URL</span></span>

-   <span data-ttu-id="4f8bc-398">Azure Monitor URL</span><span class="sxs-lookup"><span data-stu-id="4f8bc-398">Azure Monitor URL</span></span>

-   <span data-ttu-id="4f8bc-399">Data URL</span><span class="sxs-lookup"><span data-stu-id="4f8bc-399">Data URL</span></span>

-   <span data-ttu-id="4f8bc-400">VNet Gateway Resource Id (optional)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-400">VNet Gateway Resource Id (optional)</span></span>

##### <a name="confirmation-email"></a><span data-ttu-id="4f8bc-401">Confirmation Email</span><span class="sxs-lookup"><span data-stu-id="4f8bc-401">Confirmation Email</span></span> 

<span data-ttu-id="4f8bc-402">If you provide an email address ([Basics Section](#basics)), an email would be sent to the email address with the deployment output information.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-402">If you provide an email address ([Basics Section](#basics)), an email would be sent to the email address with the deployment output information.</span></span>

![deployment email](./media/ethereum-poa-deployment-guide/deployment-email.png)

##### <a name="portal"></a><span data-ttu-id="4f8bc-404">Portal</span><span class="sxs-lookup"><span data-stu-id="4f8bc-404">Portal</span></span>

<span data-ttu-id="4f8bc-405">Once the deployment has completed successfully and all resources have been provisioned you'll be able to view the output parameters in your resource group.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-405">Once the deployment has completed successfully and all resources have been provisioned you'll be able to view the output parameters in your resource group.</span></span>

1.  <span data-ttu-id="4f8bc-406">Locate your resource group in the portal</span><span class="sxs-lookup"><span data-stu-id="4f8bc-406">Locate your resource group in the portal</span></span>

2.  <span data-ttu-id="4f8bc-407">Navigate to *Deployments*</span><span class="sxs-lookup"><span data-stu-id="4f8bc-407">Navigate to *Deployments*</span></span>

3.  <span data-ttu-id="4f8bc-408">Select the top deployment with the same name as your resource group</span><span class="sxs-lookup"><span data-stu-id="4f8bc-408">Select the top deployment with the same name as your resource group</span></span>

4.  <span data-ttu-id="4f8bc-409">Select *Outputs*</span><span class="sxs-lookup"><span data-stu-id="4f8bc-409">Select *Outputs*</span></span>

### <a name="growing-the-consortium"></a><span data-ttu-id="4f8bc-410">Growing the consortium</span><span class="sxs-lookup"><span data-stu-id="4f8bc-410">Growing the consortium</span></span>

<span data-ttu-id="4f8bc-411">To expand your consortium, you must first connect the physical network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-411">To expand your consortium, you must first connect the physical network.</span></span>
<span data-ttu-id="4f8bc-412">Using the Public IP-based deployment this first step is seamless.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-412">Using the Public IP-based deployment this first step is seamless.</span></span> <span data-ttu-id="4f8bc-413">If deploying behind a VPN, see the section [Connecting VNet Gateway](#connecting-vnet-gateways) to perform the network connection as part of [Step 2](#step-2-new-admin-deployment).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-413">If deploying behind a VPN, see the section [Connecting VNet Gateway](#connecting-vnet-gateways) to perform the network connection as part of [Step 2](#step-2-new-admin-deployment).</span></span>

#### <a name="step-1-add-the-new-admin"></a><span data-ttu-id="4f8bc-414">Step 1: Add the new admin</span><span class="sxs-lookup"><span data-stu-id="4f8bc-414">Step 1: Add the new admin</span></span>

1.  <span data-ttu-id="4f8bc-415">Collect the new admin's public Ethereum address.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-415">Collect the new admin's public Ethereum address.</span></span>

2.  <span data-ttu-id="4f8bc-416">Navigate to the Governance DApp and create a new admin with the Ethereum address and an appropriate alias</span><span class="sxs-lookup"><span data-stu-id="4f8bc-416">Navigate to the Governance DApp and create a new admin with the Ethereum address and an appropriate alias</span></span>

3.  <span data-ttu-id="4f8bc-417">Notify the other existing members of the new request so that they can vote to add this new admin</span><span class="sxs-lookup"><span data-stu-id="4f8bc-417">Notify the other existing members of the new request so that they can vote to add this new admin</span></span>

4.  <span data-ttu-id="4f8bc-418">Once the vote reaches the 51%, the member will be added as an admin</span><span class="sxs-lookup"><span data-stu-id="4f8bc-418">Once the vote reaches the 51%, the member will be added as an admin</span></span>

![adding admin](./media/ethereum-poa-deployment-guide/adding-admin.png)

#### <a name="step-2-new-admin-deployment"></a><span data-ttu-id="4f8bc-420">Step 2: New admin deployment</span><span class="sxs-lookup"><span data-stu-id="4f8bc-420">Step 2: New admin deployment</span></span>

1.  <span data-ttu-id="4f8bc-421">Share the following information with the joining member.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-421">Share the following information with the joining member.</span></span> <span data-ttu-id="4f8bc-422">This information can be found in your post-deployment email or in the portal deployment output.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-422">This information can be found in your post-deployment email or in the portal deployment output.</span></span>

    -  <span data-ttu-id="4f8bc-423">Consortium Data Url</span><span class="sxs-lookup"><span data-stu-id="4f8bc-423">Consortium Data Url</span></span>

    -  <span data-ttu-id="4f8bc-424">The number of nodes you've deployed</span><span class="sxs-lookup"><span data-stu-id="4f8bc-424">The number of nodes you've deployed</span></span>

    -  <span data-ttu-id="4f8bc-425">VNet Gateway Resource Id (if using VPN)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-425">VNet Gateway Resource Id (if using VPN)</span></span>

2.  <span data-ttu-id="4f8bc-426">The deploying member should use the [same solution](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) when deploying their network presence with keeping the following in mind:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-426">The deploying member should use the [same solution](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) when deploying their network presence with keeping the following in mind:</span></span>

    -  <span data-ttu-id="4f8bc-427">Select *Join Existing*</span><span class="sxs-lookup"><span data-stu-id="4f8bc-427">Select *Join Existing*</span></span>

    -  <span data-ttu-id="4f8bc-428">Choose the same number of validator nodes as the rest of the  members on the network to ensure fair representation</span><span class="sxs-lookup"><span data-stu-id="4f8bc-428">Choose the same number of validator nodes as the rest of the  members on the network to ensure fair representation</span></span>

    -  <span data-ttu-id="4f8bc-429">Use the same Ethereum address that was provided in the [previous  step](#step-1-add-the-new-admin)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-429">Use the same Ethereum address that was provided in the [previous  step](#step-1-add-the-new-admin)</span></span>

    -  <span data-ttu-id="4f8bc-430">Pass in the provided *Consortium Data Url* on the *Ethereum  Settings* tab</span><span class="sxs-lookup"><span data-stu-id="4f8bc-430">Pass in the provided *Consortium Data Url* on the *Ethereum  Settings* tab</span></span>

    -  <span data-ttu-id="4f8bc-431">If the rest of the network is behind a VPN, select *Private  VNet* under the advanced section</span><span class="sxs-lookup"><span data-stu-id="4f8bc-431">If the rest of the network is behind a VPN, select *Private  VNet* under the advanced section</span></span>

#### <a name="step-3-delegate-validators"></a><span data-ttu-id="4f8bc-432">Step 3: Delegate validators</span><span class="sxs-lookup"><span data-stu-id="4f8bc-432">Step 3: Delegate validators</span></span>

<span data-ttu-id="4f8bc-433">The new admin will need to authorize the validators to participate on their behalf.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-433">The new admin will need to authorize the validators to participate on their behalf.</span></span> <span data-ttu-id="4f8bc-434">This cannot be done automatically since only the member controls their keys.\*</span><span class="sxs-lookup"><span data-stu-id="4f8bc-434">This cannot be done automatically since only the member controls their keys.\*</span></span>

<span data-ttu-id="4f8bc-435">_\*The first member's nodes on the network can automatically be added because we can precompile their validator nodes into the genesis block on the network._</span><span class="sxs-lookup"><span data-stu-id="4f8bc-435">_\*The first member's nodes on the network can automatically be added because we can precompile their validator nodes into the genesis block on the network._</span></span>

<span data-ttu-id="4f8bc-436">The new admin must perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-436">The new admin must perform the following steps:</span></span>

1.  <span data-ttu-id="4f8bc-437">Open the Governance DApp deployed as part of *their* deployment</span><span class="sxs-lookup"><span data-stu-id="4f8bc-437">Open the Governance DApp deployed as part of *their* deployment</span></span>

2.  <span data-ttu-id="4f8bc-438">Navigate to the Validators tab</span><span class="sxs-lookup"><span data-stu-id="4f8bc-438">Navigate to the Validators tab</span></span>

3.  <span data-ttu-id="4f8bc-439">Select each of the validators that have been deployed and click **Add**</span><span class="sxs-lookup"><span data-stu-id="4f8bc-439">Select each of the validators that have been deployed and click **Add**</span></span>

![adding validators](./media/ethereum-poa-deployment-guide/adding-validators.png)

#### <a name="connecting-vnet-gateways"></a><span data-ttu-id="4f8bc-441">Connecting VNet gateways</span><span class="sxs-lookup"><span data-stu-id="4f8bc-441">Connecting VNet gateways</span></span>

<span data-ttu-id="4f8bc-442">In the case of a private network, the different members are connected via VNet gateway connections.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-442">In the case of a private network, the different members are connected via VNet gateway connections.</span></span> <span data-ttu-id="4f8bc-443">Before a member can join the network and see transaction traffic, an existing member must perform a final configuration on their VPN gateway to accept the connection.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-443">Before a member can join the network and see transaction traffic, an existing member must perform a final configuration on their VPN gateway to accept the connection.</span></span> <span data-ttu-id="4f8bc-444">This means that the Ethereum nodes of the joining member will not run until a connection is established.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-444">This means that the Ethereum nodes of the joining member will not run until a connection is established.</span></span> <span data-ttu-id="4f8bc-445">It is recommended to create redundant network connections (mesh) into the consortium to reduce chances of a single point of failure.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-445">It is recommended to create redundant network connections (mesh) into the consortium to reduce chances of a single point of failure.</span></span>

<span data-ttu-id="4f8bc-446">After the new member deploys, the existing member must complete the bi-directional connection by setting up a VNet gateway connection to the new member.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-446">After the new member deploys, the existing member must complete the bi-directional connection by setting up a VNet gateway connection to the new member.</span></span> <span data-ttu-id="4f8bc-447">To achieve this existing member will need:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-447">To achieve this existing member will need:</span></span>

1.  <span data-ttu-id="4f8bc-448">The VNet gateway ResourceId of the connecting member (see deployment output)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-448">The VNet gateway ResourceId of the connecting member (see deployment output)</span></span>

2.  <span data-ttu-id="4f8bc-449">The shared connection key</span><span class="sxs-lookup"><span data-stu-id="4f8bc-449">The shared connection key</span></span>

<span data-ttu-id="4f8bc-450">The existing member must run the following PowerShell script to complete the connection.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-450">The existing member must run the following PowerShell script to complete the connection.</span></span> <span data-ttu-id="4f8bc-451">We recommend using Azure Cloud Shell located in the top right navigation bar in the portal.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-451">We recommend using Azure Cloud Shell located in the top right navigation bar in the portal.</span></span>

![cloud shell](./media/ethereum-poa-deployment-guide/cloud-shell.png)

```bash
$MyGatewayResourceId = "<EXISTING_MEMBER_RESOURCEID>"
$OtherGatewayResourceId = "<NEW_MEMBER_RESOURCEID]"
$ConnectionName = "Leader2Member"
$SharedKey = "<NEW_MEMBER_KEY>"

## $myGatewayResourceId tells me what subscription I am in, what ResourceGroup and the VNetGatewayName
$splitValue = $MyGatewayResourceId.Split('/')
$MySubscriptionid = $splitValue[2]
$MyResourceGroup = $splitValue[4]
$MyGatewayName = $splitValue[8]

## $otherGatewayResourceid tells me what the subscription and VNet GatewayName are
$OtherGatewayName = $OtherGatewayResourceId.Split('/')[8]
$Subscription=Select-AzureRmSubscription -SubscriptionId $MySubscriptionid

## create a PSVirtualNetworkGateway instance for the gateway I want to connect to
$OtherGateway=New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
$OtherGateway.Name = $OtherGatewayName
$OtherGateway.Id = $OtherGatewayResourceId
$OtherGateway.GatewayType = "Vpn"
$OtherGateway.VpnType = "RouteBased"

## get a PSVirtualNetworkGateway instance for my gateway
$MyGateway = Get-AzureRmVirtualNetworkGateway -Name $MyGatewayName -ResourceGroupName $MyResourceGroup

## create the connection
New-AzureRmVirtualNetworkGatewayConnection -Name $ConnectionName -ResourceGroupName $MyResourceGroup -VirtualNetworkGateway1 $MyGateway -VirtualNetworkGateway2 $OtherGateway -Location $MyGateway.Location -ConnectionType Vnet2Vnet -SharedKey $SharedKey -EnableBgp $True
```

### <a name="service-monitoring"></a><span data-ttu-id="4f8bc-453">Service monitoring</span><span class="sxs-lookup"><span data-stu-id="4f8bc-453">Service monitoring</span></span>

<span data-ttu-id="4f8bc-454">You can locate your Azure Monitor portal either by following the link in the deployment email or locating the parameter in the deployment output \[OMS\_PORTAL\_URL\].</span><span class="sxs-lookup"><span data-stu-id="4f8bc-454">You can locate your Azure Monitor portal either by following the link in the deployment email or locating the parameter in the deployment output \[OMS\_PORTAL\_URL\].</span></span>

<span data-ttu-id="4f8bc-455">The portal will first display high-level network statistics and node overview.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-455">The portal will first display high-level network statistics and node overview.</span></span>

![monitor categories](./media/ethereum-poa-deployment-guide/monitor-categories.png)

<span data-ttu-id="4f8bc-457">Selecting **Node Overview** will direct you to a portal to view per-node infrastructure statistics.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-457">Selecting **Node Overview** will direct you to a portal to view per-node infrastructure statistics.</span></span>

![node stats](./media/ethereum-poa-deployment-guide/node-stats.png)

<span data-ttu-id="4f8bc-459">Selecting **Network Stats** will direct you to view Ethereum network statistics.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-459">Selecting **Network Stats** will direct you to view Ethereum network statistics.</span></span>

![network stats](./media/ethereum-poa-deployment-guide/network-stats.png)

#### <a name="sample-log-analytics-queries"></a><span data-ttu-id="4f8bc-461">Sample Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="4f8bc-461">Sample Log Analytics queries</span></span>

<span data-ttu-id="4f8bc-462">Behind these dashboards is a set of queryable raw logs.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-462">Behind these dashboards is a set of queryable raw logs.</span></span> <span data-ttu-id="4f8bc-463">You can use these raw logs to customize the dashboards, investigate failures, or setup threshold alerting.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-463">You can use these raw logs to customize the dashboards, investigate failures, or setup threshold alerting.</span></span> <span data-ttu-id="4f8bc-464">Below you'll find a set of example queries that can be ran in the Log Search tool:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-464">Below you'll find a set of example queries that can be ran in the Log Search tool:</span></span>

##### <a name="lists-blocks-that-have-been-reported-by-more-than-one-validator-useful-to-help-find-chain-forks"></a><span data-ttu-id="4f8bc-465">Lists blocks that have been reported by more than one validator.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-465">Lists blocks that have been reported by more than one validator.</span></span> <span data-ttu-id="4f8bc-466">Useful to help find chain forks.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-466">Useful to help find chain forks.</span></span>

```sql
MinedBlock_CL
| summarize DistinctMiners = dcount(BlockMiner_s) by BlockNumber_d, BlockMiner_s
| where DistinctMiners > 1
```

##### <a name="get-average-peer-count-for-a-specified-validator-node-averaged-over-5-minute-buckets"></a><span data-ttu-id="4f8bc-467">Get average peer count for a specified validator node averaged over 5 minute buckets.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-467">Get average peer count for a specified validator node averaged over 5 minute buckets.</span></span>

```sql
let PeerCountRegex = @"Syncing with peers: (\d+) active, (\d+) confirmed, (\d+)";
ParityLog_CL
| where Computer == "vl-devn3lgdm-reg1000001"
| project RawData, TimeGenerated
| where RawData matches regex PeerCountRegex
| extend ActivePeers = extract(PeerCountRegex, 1, RawData, typeof(int)) 
| summarize avg(ActivePeers) by bin(TimeGenerated, 5m)
```

### <a name="ssh-access"></a><span data-ttu-id="4f8bc-468">SSH access</span><span class="sxs-lookup"><span data-stu-id="4f8bc-468">SSH access</span></span>

<span data-ttu-id="4f8bc-469">For security reasons, the SSH port access is denied by a network group security rule by default.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-469">For security reasons, the SSH port access is denied by a network group security rule by default.</span></span> <span data-ttu-id="4f8bc-470">To access the virtual machine scale set instances in the PoA network, you will need to change this rule to \"Allow\"</span><span class="sxs-lookup"><span data-stu-id="4f8bc-470">To access the virtual machine scale set instances in the PoA network, you will need to change this rule to \"Allow\"</span></span>

1.  <span data-ttu-id="4f8bc-471">Start in the Overview section of the deployed resource group from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-471">Start in the Overview section of the deployed resource group from Azure portal.</span></span>

    ![ssh overview](./media/ethereum-poa-deployment-guide/ssh-overview.png)

2.  <span data-ttu-id="4f8bc-473">Select the Network Security Group</span><span class="sxs-lookup"><span data-stu-id="4f8bc-473">Select the Network Security Group</span></span>

    ![ssh nsg](./media/ethereum-poa-deployment-guide/ssh-nsg.png)

3.  <span data-ttu-id="4f8bc-475">Select the \"allow-ssh\" rule</span><span class="sxs-lookup"><span data-stu-id="4f8bc-475">Select the \"allow-ssh\" rule</span></span>

    ![ssh-allow](./media/ethereum-poa-deployment-guide/ssh-allow.png)

4.  <span data-ttu-id="4f8bc-477">Change \"Action\" to Allow</span><span class="sxs-lookup"><span data-stu-id="4f8bc-477">Change \"Action\" to Allow</span></span>

    ![ssh enable allow](./media/ethereum-poa-deployment-guide/ssh-enable-allow.png)

5.  <span data-ttu-id="4f8bc-479">Click \"Save\" (Changes may take a few minutes to apply)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-479">Click \"Save\" (Changes may take a few minutes to apply)</span></span>

<span data-ttu-id="4f8bc-480">You can now remotely connect to the virtual machines for the validator nodes via SSH with your provided admin username and password/SSH key.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-480">You can now remotely connect to the virtual machines for the validator nodes via SSH with your provided admin username and password/SSH key.</span></span>
<span data-ttu-id="4f8bc-481">The SSH command to run to access the first validator node is listed in the template deployment output parameter as, 'SSH\_TO\_FIRST\_VL\_NODE\_REGION1' (for the sample deployment: ssh - p 4000 poaadmin\@leader4vb.eastus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-481">The SSH command to run to access the first validator node is listed in the template deployment output parameter as, 'SSH\_TO\_FIRST\_VL\_NODE\_REGION1' (for the sample deployment: ssh - p 4000 poaadmin\@leader4vb.eastus.cloudapp.azure.com).</span></span> <span data-ttu-id="4f8bc-482">To get to additional transaction nodes, increment the port number by one (For example, the first transaction node is on port 4000).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-482">To get to additional transaction nodes, increment the port number by one (For example, the first transaction node is on port 4000).</span></span>

<span data-ttu-id="4f8bc-483">If you deployed to more than one region, change the above command to the DNS name or IP address of the load balancer in that region.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-483">If you deployed to more than one region, change the above command to the DNS name or IP address of the load balancer in that region.</span></span> <span data-ttu-id="4f8bc-484">To find the DNS name or IP address of the other regions, find the resource with the naming convention \*\*\*\*\*-lbpip-reg\#, and view its DNS name and IP address properties.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-484">To find the DNS name or IP address of the other regions, find the resource with the naming convention \*\*\*\*\*-lbpip-reg\#, and view its DNS name and IP address properties.</span></span>

### <a name="azure-traffic-manager-load-balancing"></a><span data-ttu-id="4f8bc-485">Azure Traffic Manager load balancing</span><span class="sxs-lookup"><span data-stu-id="4f8bc-485">Azure Traffic Manager load balancing</span></span>

<span data-ttu-id="4f8bc-486">Azure Traffic Manager can help reduce downtime and improve responsiveness of the PoA network by routing incoming traffic across multiple deployments in different regions.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-486">Azure Traffic Manager can help reduce downtime and improve responsiveness of the PoA network by routing incoming traffic across multiple deployments in different regions.</span></span> <span data-ttu-id="4f8bc-487">Built-in health checks and automatic re-routing help ensure high availability of the RPC endpoints and the Governance DApp.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-487">Built-in health checks and automatic re-routing help ensure high availability of the RPC endpoints and the Governance DApp.</span></span> <span data-ttu-id="4f8bc-488">This feature is useful if you have deployed to multiple regions and are production ready.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-488">This feature is useful if you have deployed to multiple regions and are production ready.</span></span>

<span data-ttu-id="4f8bc-489">Use Traffic Manager to:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-489">Use Traffic Manager to:</span></span>

-   <span data-ttu-id="4f8bc-490">Improve PoA network availability with automatic failover.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-490">Improve PoA network availability with automatic failover.</span></span>

-   <span data-ttu-id="4f8bc-491">Increase your networks responsiveness by routing end users to the Azure location with lowest network latency.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-491">Increase your networks responsiveness by routing end users to the Azure location with lowest network latency.</span></span>

<span data-ttu-id="4f8bc-492">If you decide to create a Traffic Manager profile, you can use the DNS name of the profile to access your network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-492">If you decide to create a Traffic Manager profile, you can use the DNS name of the profile to access your network.</span></span> <span data-ttu-id="4f8bc-493">Once other consortium members have been added to the network, the Traffic Manager can also be used to load balance across their deployed validators.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-493">Once other consortium members have been added to the network, the Traffic Manager can also be used to load balance across their deployed validators.</span></span>

#### <a name="creating-a-traffic-manager-profile"></a><span data-ttu-id="4f8bc-494">Creating a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="4f8bc-494">Creating a Traffic Manager profile</span></span>

<span data-ttu-id="4f8bc-495">Search for and select \"Traffic Manager profile\" after clicking the \"Create a resource\" button in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-495">Search for and select \"Traffic Manager profile\" after clicking the \"Create a resource\" button in the Azure portal.</span></span>

![search for azure traffic manager](./media/ethereum-poa-deployment-guide/traffic-manager-search.png)

<span data-ttu-id="4f8bc-497">Give the profile a unique name and select the Resource Group that was created during the PoA deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-497">Give the profile a unique name and select the Resource Group that was created during the PoA deployment.</span></span>

![create traffic manager](./media/ethereum-poa-deployment-guide/traffic-manager-create.png)

<span data-ttu-id="4f8bc-499">Once it is deployed, then select the instance in the resource group.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-499">Once it is deployed, then select the instance in the resource group.</span></span> <span data-ttu-id="4f8bc-500">The DNS name to access the traffic manager can be found in the Overview tab</span><span class="sxs-lookup"><span data-stu-id="4f8bc-500">The DNS name to access the traffic manager can be found in the Overview tab</span></span>

![Locate traffic manager DNS](./media/ethereum-poa-deployment-guide/traffic-manager-dns.png)

<span data-ttu-id="4f8bc-502">Select the Endpoints tab and click the Add button.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-502">Select the Endpoints tab and click the Add button.</span></span> <span data-ttu-id="4f8bc-503">Then change the Target resource type to Public IP address.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-503">Then change the Target resource type to Public IP address.</span></span> <span data-ttu-id="4f8bc-504">Then select the public IP address of the first region\'s load balancer.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-504">Then select the public IP address of the first region\'s load balancer.</span></span>

![Routing traffic manager](./media/ethereum-poa-deployment-guide/traffic-manager-routing.png)

<span data-ttu-id="4f8bc-506">Repeat for each region in the deployed network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-506">Repeat for each region in the deployed network.</span></span> <span data-ttu-id="4f8bc-507">Once the endpoints are in the \"enabled\" status, they will be automatically load and region balanced at the DNS name of the traffic manager.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-507">Once the endpoints are in the \"enabled\" status, they will be automatically load and region balanced at the DNS name of the traffic manager.</span></span> <span data-ttu-id="4f8bc-508">You can now use this DNS name in place of the \[CONSORTIUM\_DATA\_URL\] parameter in other steps of the document.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-508">You can now use this DNS name in place of the \[CONSORTIUM\_DATA\_URL\] parameter in other steps of the document.</span></span>

## <a name="data-api"></a><span data-ttu-id="4f8bc-509">Data API</span><span class="sxs-lookup"><span data-stu-id="4f8bc-509">Data API</span></span>

<span data-ttu-id="4f8bc-510">Each consortium member hosts the necessary information for others to connect to the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-510">Each consortium member hosts the necessary information for others to connect to the network.</span></span> <span data-ttu-id="4f8bc-511">The existing member will provide the [CONSORTIUM_DATA_URL] prior to the member's deployment.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-511">The existing member will provide the [CONSORTIUM_DATA_URL] prior to the member's deployment.</span></span> <span data-ttu-id="4f8bc-512">Upon deployment, a joining member will retrieve information from the JSON interface at the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-512">Upon deployment, a joining member will retrieve information from the JSON interface at the following endpoint:</span></span>

`<CONSORTIUM_DATA_URL>/networkinfo`

<span data-ttu-id="4f8bc-513">The response will contain information useful for joining members (Genesis block, Validator Set contract ABI, bootnodes) as well as information useful to the existing member (validator addresses).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-513">The response will contain information useful for joining members (Genesis block, Validator Set contract ABI, bootnodes) as well as information useful to the existing member (validator addresses).</span></span> <span data-ttu-id="4f8bc-514">We encourage use of this standardization to extend the consortium across cloud providers.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-514">We encourage use of this standardization to extend the consortium across cloud providers.</span></span> <span data-ttu-id="4f8bc-515">This API will return a JSON formatted response with the following structure:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-515">This API will return a JSON formatted response with the following structure:</span></span>
```json
{
  "$id": "", 
  "type": "object", 
  "definitions": {}, 
  "$schema": "http://json-schema.org/draft-07/schema#", 
  "properties": {
    "majorVersion": {
      "$id": "/properties/majorVersion", 
      "type": "integer", 
      "title": "This schema’s major version", 
      "default": 0, 
      "examples": [
        0
      ]
    }, 
    "minorVersion": {
      "$id": "/properties/minorVersion", 
      "type": "integer", 
      "title": "This schema’s minor version", 
      "default": 0, 
      "examples": [
        0
      ]
    }, 
    "bootnodes": {
      "$id": "/properties/bootnodes", 
      "type": "array", 
      "items": {
        "$id": "/properties/bootnodes/items", 
        "type": "string", 
        "title": "This member’s bootnodes", 
        "default": "", 
        "examples": [
          "enode://a348586f0fb0516c19de75bf54ca930a08f1594b7202020810b72c5f8d90635189d72d8b96f306f08761d576836a6bfce112cfb6ae6a3330588260f79a3d0ecb@10.1.17.5:30300", 
          "enode://2d8474289af0bb38e3600a7a481734b2ab19d4eaf719f698fe885fb239f5d33faf217a860b170e2763b67c2f18d91c41272de37ac67386f80d1de57a3d58ddf2@10.1.17.4:30300"
        ]
      }
    }, 
    "valSetContract": {
      "$id": "/properties/valSetContract", 
      "type": "string", 
      "title": "The ValidatorSet Contract Source", 
      "default": "", 
      "examples": [
        "pragma solidity 0.4.21;\n\nimport \"./SafeMath.sol\";\nimport \"./Utils.sol\";\n\ncontract ValidatorSet …"
      ]
    }, 
    "adminContract": {
      "$id": "/properties/adminContract", 
      "type": "string", 
      "title": "The AdminSet Contract Source", 
      "default": "", 
      "examples": [
        "pragma solidity 0.4.21;\nimport \"./SafeMath.sol\";\nimport \"./SimpleValidatorSet.sol\";\nimport \"./Admin.sol\";\n\ncontract AdminValidatorSet is SimpleValidatorSet { …"
      ]
    }, 
    "adminContractABI": {
      "$id": "/properties/adminContractABI", 
      "type": "string", 
      "title": "The Admin Contract ABI", 
      "default": "", 
      "examples": [
        "[{\"constant\":false,\"inputs\":[{\"name\":\"proposedAdminAddress\",\"type\":\"address\"},…"
      ]
    }, 
    "paritySpec": {
      "$id": "/properties/paritySpec", 
      "type": "string", 
      "title": "The Parity client spec file", 
      "default": "", 
      "examples": [
        "\n{\n \"name\": \"PoA\",\n \"engine\": {\n \"authorityRound\": {\n \"params\": {\n \"stepDuration\": \"2\",\n \"validators\" : {\n \"safeContract\": \"0x0000000000000000000000000000000000000006\"\n },\n \"gasLimitBoundDivisor\": \"0x400\",\n \"maximumExtraDataSize\": \"0x2A\",\n \"minGasLimit\": \"0x2FAF080\",\n \"networkID\" : \"0x9a2112\"\n }\n }\n },\n \"params\": {\n \"gasLimitBoundDivisor\": \"0x400\",\n \"maximumExtraDataSize\": \"0x2A\",\n \"minGasLimit\": \"0x2FAF080\",\n \"networkID\" : \"0x9a2112\",\n \"wasmActivationTransition\": \"0x0\"\n },\n \"genesis\": {\n \"seal\": {\n \"authorityRound\": {\n \"step\": \"0x0\",\n \"signature\": \"0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000\"\n }\n },\n \"difficulty\": \"0x20000\",\n \"gasLimit\": \"0x2FAF080\"\n },\n \"accounts\": {\n \"0x0000000000000000000000000000000000000001\": { \"balance\": \"1\", \"builtin\": { \"name\": \"ecrecover\", \"pricing\": { \"linear\": { \"base\": 3000, \"word\": 0 } } } },\n \"0x0000000000000000000000000000000000000002\": { \"balance\": \"1\", \"builtin\": { \"name\": \"sha256\", \"pricing\": { \"linear\": { \"base\": 60, \"word\": 12 } } } },\n \"0x0000000000000000000000000000000000000003\": { \"balance\": \"1\", \"builtin\": { \"name\": \"ripemd160\", \"pricing\": { \"linear\": { \"base\": 600, \"word\": 120 } } } },\n \"0x0000000000000000000000000000000000000004\": { \"balance\": \"1\", \"builtin\": { \"name\": \"identity\", \"pricing\": { \"linear\": { \"base\": 15, \"word\": 3 } } } },\n \"0x0000000000000000000000000000000000000006\": { \"balance\": \"0\", \"constructor\" : \"…\" }\n }\n}"
      ]
    }, 
    "errorMessage": {
      "$id": "/properties/errorMessage", 
      "type": "string", 
      "title": "Error message", 
      "default": "", 
      "examples": [
        ""
      ]
    }, 
    "addressList": {
      "$id": "/properties/addressList", 
      "type": "object", 
      "properties": {
        "addresses": {
          "$id": "/properties/addressList/properties/addresses", 
          "type": "array", 
          "items": {
            "$id": "/properties/addressList/properties/addresses/items", 
            "type": "string", 
            "title": "This member’s validator addresses", 
            "default": "", 
            "examples": [
              "0x00a3cff0dccc0ecb6ae0461045e0e467cff4805f", 
              "0x009ce13a7b2532cbd89b2d28cecd75f7cc8c0727"
            ]
          }
        }
      }
    }
  }
}

```
## <a name="development"></a><span data-ttu-id="4f8bc-516">Development</span><span class="sxs-lookup"><span data-stu-id="4f8bc-516">Development</span></span>

### <a name="programmatically-interacting-with-a-smart-contract"></a><span data-ttu-id="4f8bc-517">Programmatically interacting with a smart contract</span><span class="sxs-lookup"><span data-stu-id="4f8bc-517">Programmatically interacting with a smart contract</span></span>

> [!WARNING]
> <span data-ttu-id="4f8bc-518">Never send your Ethereum private key over the network!</span><span class="sxs-lookup"><span data-stu-id="4f8bc-518">Never send your Ethereum private key over the network!</span></span> <span data-ttu-id="4f8bc-519">Ensure that each transaction is signed locally first and the signed transaction is sent over the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-519">Ensure that each transaction is signed locally first and the signed transaction is sent over the network.</span></span>

<span data-ttu-id="4f8bc-520">In the following example, we use *ethereumjs-wallet* to generate an Ethereum address, *ethereumjs-tx* to sign locally, and *web3* to send the raw transaction to the Ethereum RPC endpoint.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-520">In the following example, we use *ethereumjs-wallet* to generate an Ethereum address, *ethereumjs-tx* to sign locally, and *web3* to send the raw transaction to the Ethereum RPC endpoint.</span></span>

<span data-ttu-id="4f8bc-521">We'll use this simple Hello-World smart contract for this example:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-521">We'll use this simple Hello-World smart contract for this example:</span></span>

```javascript
pragma solidity ^0.4.11;
contract postBox {
    string message;
    function postMsg(string text) public {
        message = text; 
    }
    function getMsg() public view returns (string) {
        return message;
    }
}
```

<span data-ttu-id="4f8bc-522">This example assumes the contract is already deployed.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-522">This example assumes the contract is already deployed.</span></span> <span data-ttu-id="4f8bc-523">You can use *solc* and *web3* for deploying a contract programmatically.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-523">You can use *solc* and *web3* for deploying a contract programmatically.</span></span> <span data-ttu-id="4f8bc-524">First install the following node modules:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-524">First install the following node modules:</span></span>
```
sudo npm install web3@0.20.2
sudo npm install ethereumjs-tx@1.3.6
sudo npm install ethereumjs-wallet@0.6.1
```
<span data-ttu-id="4f8bc-525">This nodeJS script will perform the following:</span><span class="sxs-lookup"><span data-stu-id="4f8bc-525">This nodeJS script will perform the following:</span></span>

-   <span data-ttu-id="4f8bc-526">Construct a raw transaction: postMsg</span><span class="sxs-lookup"><span data-stu-id="4f8bc-526">Construct a raw transaction: postMsg</span></span>

-   <span data-ttu-id="4f8bc-527">Sign the transaction using the generated private key</span><span class="sxs-lookup"><span data-stu-id="4f8bc-527">Sign the transaction using the generated private key</span></span>

-   <span data-ttu-id="4f8bc-528">Submit the signed transaction to the Ethereum network</span><span class="sxs-lookup"><span data-stu-id="4f8bc-528">Submit the signed transaction to the Ethereum network</span></span>

```javascript
var ethereumjs = require('ethereumjs-tx')
var wallet = require('ethereumjs-wallet')
var Web3 = require('web3')

// TODO Replace with your contract address
var address = "0xfe53559f5f7a77125039a993e8d5d9c2901edc58";
var abi = [{"constant": false,"inputs": [{"name": "text","type": "string"}],"name": "postMsg","outputs": [],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": true,"inputs": [],"name": "getMsg","outputs": [{"name": "","type": "string"}],"payable": false,"stateMutability": "view","type": "function"}];

// Generate a new Ethereum account
var account = wallet.generate();
var accountAddress = account.getAddressString()
var privateKey = account.getPrivateKey();

 // TODO Replace with your RPC endpoint
 var web3 = new Web3(new Web3.providers.HttpProvider(
    "http://testzvdky-dns-reg1.eastus.cloudapp.azure.com:8545"));
 
// Get the current nonce of the account
 web3.eth.getTransactionCount(accountAddress, function (err, nonce) {
   var data = web3.eth.contract(abi).at(address).postMsg.getData("Hello World");
   var rawTx = {
     nonce: nonce,
     gasPrice: '0x00', 
     gasLimit: '0x2FAF080',
     to: address, 
     value: '0x00', 
     data: data
   }
   var tx = new ethereumjs(rawTx);
   
   tx.sign(privateKey);

   var raw = '0x' + tx.serialize().toString('hex');
   web3.eth.sendRawTransaction(raw, function (txErr, transactionHash) {
     console.log("TX Hash: " + transactionHash);
     console.log("Error: " + txErr);
   });
 });
```

### <a name="debug-a-smart-contract-truffle-develop"></a><span data-ttu-id="4f8bc-529">Debug a smart contract (Truffle Develop)</span><span class="sxs-lookup"><span data-stu-id="4f8bc-529">Debug a smart contract (Truffle Develop)</span></span>

<span data-ttu-id="4f8bc-530">Truffle has a local develop network that is available for debugging smart contract.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-530">Truffle has a local develop network that is available for debugging smart contract.</span></span> <span data-ttu-id="4f8bc-531">You can find the full tutorial [here](http://truffleframework.com/tutorials/debugging-a-smart-contract).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-531">You can find the full tutorial [here](http://truffleframework.com/tutorials/debugging-a-smart-contract).</span></span>

### <a name="webassembly-wasm-support"></a><span data-ttu-id="4f8bc-532">WebAssembly (WASM) support</span><span class="sxs-lookup"><span data-stu-id="4f8bc-532">WebAssembly (WASM) support</span></span>

<span data-ttu-id="4f8bc-533">WebAssembly support is already enabled for you on newly deployed PoA networks.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-533">WebAssembly support is already enabled for you on newly deployed PoA networks.</span></span> <span data-ttu-id="4f8bc-534">It allows for smart-contract development in any language that transpiles to Web-Assembly (Rust, C, C++).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-534">It allows for smart-contract development in any language that transpiles to Web-Assembly (Rust, C, C++).</span></span> <span data-ttu-id="4f8bc-535">See the links below for additional information</span><span class="sxs-lookup"><span data-stu-id="4f8bc-535">See the links below for additional information</span></span>

-   <span data-ttu-id="4f8bc-536">Parity Overview of WebAssembly - <https://wiki.parity.io/WebAssembly-Home></span><span class="sxs-lookup"><span data-stu-id="4f8bc-536">Parity Overview of WebAssembly - <https://wiki.parity.io/WebAssembly-Home></span></span>

-   <span data-ttu-id="4f8bc-537">Tutorial from Parity Tech - <https://github.com/paritytech/pwasm-tutorial></span><span class="sxs-lookup"><span data-stu-id="4f8bc-537">Tutorial from Parity Tech - <https://github.com/paritytech/pwasm-tutorial></span></span>

## <a name="faq"></a><span data-ttu-id="4f8bc-538">FAQ</span><span class="sxs-lookup"><span data-stu-id="4f8bc-538">FAQ</span></span>

### <a name="i-notice-a-bunch-of-transactions-on-the-network-that-i-didnt-send-where-are-these-coming-from"></a><span data-ttu-id="4f8bc-539">I notice a bunch of transactions on the network that I didn\'t send.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-539">I notice a bunch of transactions on the network that I didn\'t send.</span></span> <span data-ttu-id="4f8bc-540">Where are these coming from?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-540">Where are these coming from?</span></span>

<span data-ttu-id="4f8bc-541">It is insecure to unlock the [personal API](https://web3js.readthedocs.io/en/1.0/web3-eth-personal.html).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-541">It is insecure to unlock the [personal API](https://web3js.readthedocs.io/en/1.0/web3-eth-personal.html).</span></span> <span data-ttu-id="4f8bc-542">Bot accounts are listening for unlocked Ethereum accounts and attempt to drain the funds.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-542">Bot accounts are listening for unlocked Ethereum accounts and attempt to drain the funds.</span></span> <span data-ttu-id="4f8bc-543">The bot assumes these accounts contain real-ether and attempt to be the first to siphon the balance.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-543">The bot assumes these accounts contain real-ether and attempt to be the first to siphon the balance.</span></span> <span data-ttu-id="4f8bc-544">Do not enable the personal API on the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-544">Do not enable the personal API on the network.</span></span> <span data-ttu-id="4f8bc-545">Instead pre-sign the transactions either manually using a wallet like MetaMask or programmatically as outlined in the section Programmatically Interacting with a Smart Contract.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-545">Instead pre-sign the transactions either manually using a wallet like MetaMask or programmatically as outlined in the section Programmatically Interacting with a Smart Contract.</span></span>

### <a name="how-to-ssh-onto-a-vm"></a><span data-ttu-id="4f8bc-546">How to SSH onto a VM?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-546">How to SSH onto a VM?</span></span>

<span data-ttu-id="4f8bc-547">We lock down the SSH port for security reasons.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-547">We lock down the SSH port for security reasons.</span></span> <span data-ttu-id="4f8bc-548">Follow [this guide to enable the SSH port](#_Accessing_Nodes_via).</span><span class="sxs-lookup"><span data-stu-id="4f8bc-548">Follow [this guide to enable the SSH port](#_Accessing_Nodes_via).</span></span>

### <a name="how-do-i-set-up-an-audit-member-or-transaction-nodes"></a><span data-ttu-id="4f8bc-549">How do I set up an audit member or transaction nodes?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-549">How do I set up an audit member or transaction nodes?</span></span>

<span data-ttu-id="4f8bc-550">Transaction nodes are a set of Parity clients that are peered with the network but are not participating in consensus.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-550">Transaction nodes are a set of Parity clients that are peered with the network but are not participating in consensus.</span></span> <span data-ttu-id="4f8bc-551">These nodes can still be used to submit Ethereum transactions and read the smart contract state.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-551">These nodes can still be used to submit Ethereum transactions and read the smart contract state.</span></span>
<span data-ttu-id="4f8bc-552">This works well as a mechanism for providing auditability to regulators of the network.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-552">This works well as a mechanism for providing auditability to regulators of the network.</span></span> <span data-ttu-id="4f8bc-553">To achieve this simply follow Step 2 from Growing the Consortium.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-553">To achieve this simply follow Step 2 from Growing the Consortium.</span></span>

### <a name="why-are-metamask-transactions-taking-a-long-time"></a><span data-ttu-id="4f8bc-554">Why are MetaMask transactions taking a long time?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-554">Why are MetaMask transactions taking a long time?</span></span>

<span data-ttu-id="4f8bc-555">To ensure transactions are received in the correct order, each Ethereum transaction comes with an incrementing nonce.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-555">To ensure transactions are received in the correct order, each Ethereum transaction comes with an incrementing nonce.</span></span> <span data-ttu-id="4f8bc-556">If you've used an account in MetaMask on a different network, you'll need to reset the nonce value.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-556">If you've used an account in MetaMask on a different network, you'll need to reset the nonce value.</span></span> <span data-ttu-id="4f8bc-557">Click on the settings icon (3-bars), Settings, Reset Account.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-557">Click on the settings icon (3-bars), Settings, Reset Account.</span></span> <span data-ttu-id="4f8bc-558">The transaction history will be cleared and now you can resubmit the transaction.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-558">The transaction history will be cleared and now you can resubmit the transaction.</span></span>

### <a name="are-public-ip-deployments-compatible-with-private-network-deployments"></a><span data-ttu-id="4f8bc-559">Are Public IP deployments compatible with Private network deployments?</span><span class="sxs-lookup"><span data-stu-id="4f8bc-559">Are Public IP deployments compatible with Private network deployments?</span></span>

<span data-ttu-id="4f8bc-560">No, peering requires two-way communication so the entire network must either be public or private.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-560">No, peering requires two-way communication so the entire network must either be public or private.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f8bc-561">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f8bc-561">Next steps</span></span>

<span data-ttu-id="4f8bc-562">Get started by using the [Ethereum Proof-of-Authority Consortium](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) solution.</span><span class="sxs-lookup"><span data-stu-id="4f8bc-562">Get started by using the [Ethereum Proof-of-Authority Consortium](https://portal.azure.com/?pub_source=email&pub_status=success#create/microsoft-azure-blockchain.azure-blockchain-ethereumethereum-poa-consortium) solution.</span></span>
