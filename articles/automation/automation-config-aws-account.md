---
title: Configure Authentication with Amazon Web Services  | Microsoft Docs
description: This article describes how to create and validate an AWS credential for runbooks in Azure Automation managing AWS resources.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: aws authentication, configure aws
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 81e5e5d56a7e6149409e11aca2e5fdf28d6a7134
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553890"
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a><span data-ttu-id="75e88-104">Authenticate Runbooks with Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="75e88-104">Authenticate Runbooks with Amazon Web Services</span></span>
<span data-ttu-id="75e88-105">Automating common tasks with resources in Amazon Web Services (AWS) can be accomplished with Automation runbooks in Azure.</span><span class="sxs-lookup"><span data-stu-id="75e88-105">Automating common tasks with resources in Amazon Web Services (AWS) can be accomplished with Automation runbooks in Azure.</span></span>  <span data-ttu-id="75e88-106">You can automate many tasks in AWS using Automation runbooks just like you can with resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="75e88-106">You can automate many tasks in AWS using Automation runbooks just like you can with resources in Azure.</span></span>  <span data-ttu-id="75e88-107">All that is required are two things:</span><span class="sxs-lookup"><span data-stu-id="75e88-107">All that is required are two things:</span></span>

* <span data-ttu-id="75e88-108">An AWS subscription and a set of credentials.</span><span class="sxs-lookup"><span data-stu-id="75e88-108">An AWS subscription and a set of credentials.</span></span>  <span data-ttu-id="75e88-109">Specifically your AWS Access Key and Secret Key.</span><span class="sxs-lookup"><span data-stu-id="75e88-109">Specifically your AWS Access Key and Secret Key.</span></span>  <span data-ttu-id="75e88-110">For more information, please review the article [Using AWS Credentials](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).</span><span class="sxs-lookup"><span data-stu-id="75e88-110">For more information, please review the article [Using AWS Credentials](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).</span></span>
* <span data-ttu-id="75e88-111">An Azure subscription and Automation account.</span><span class="sxs-lookup"><span data-stu-id="75e88-111">An Azure subscription and Automation account.</span></span>  <span data-ttu-id="75e88-112">For more information on setting up an Azure Automation account, please review the article [Configure Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="75e88-112">For more information on setting up an Azure Automation account, please review the article [Configure Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>  

<span data-ttu-id="75e88-113">To authenticate with AWS, you must specify a set of AWS credentials to authenticate your runbooks running from Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="75e88-113">To authenticate with AWS, you must specify a set of AWS credentials to authenticate your runbooks running from Azure Automation.</span></span> <span data-ttu-id="75e88-114">If you already have an Automation account created and you want to use that to authenticate with AWS, you can follow the steps in the following section.</span><span class="sxs-lookup"><span data-stu-id="75e88-114">If you already have an Automation account created and you want to use that to authenticate with AWS, you can follow the steps in the following section.</span></span>  <span data-ttu-id="75e88-115">If you want to dedicated an account for runbooks targetting AWS resources, you should first create a new [Automation account](automation-offering-get-started.md) (skip the option to create a service principal) and then follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="75e88-115">If you want to dedicated an account for runbooks targetting AWS resources, you should first create a new [Automation account](automation-offering-get-started.md) (skip the option to create a service principal) and then follow the steps below.</span></span>

## <a name="configure-automation-account"></a><span data-ttu-id="75e88-116">Configure Automation account</span><span class="sxs-lookup"><span data-stu-id="75e88-116">Configure Automation account</span></span>
<span data-ttu-id="75e88-117">For Azure Automation to communicate with AWS, you first need to retrieve your AWS credentials and store them as assets in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="75e88-117">For Azure Automation to communicate with AWS, you first need to retrieve your AWS credentials and store them as assets in Azure Automation.</span></span>  <span data-ttu-id="75e88-118">Perform the following steps documented in the AWS document [Managing Access Keys for your AWS Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) to create an Access Key and copy the **Access Key ID** and **Secret Access Key** (optionally download your key file to store it somewhere safe).</span><span class="sxs-lookup"><span data-stu-id="75e88-118">Perform the following steps documented in the AWS document [Managing Access Keys for your AWS Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) to create an Access Key and copy the **Access Key ID** and **Secret Access Key** (optionally download your key file to store it somewhere safe).</span></span>

<span data-ttu-id="75e88-119">After you have created and copied your AWS security keys, you need to create a Credential asset with an Azure Automation account to securely store them and reference them with your runbooks.</span><span class="sxs-lookup"><span data-stu-id="75e88-119">After you have created and copied your AWS security keys, you need to create a Credential asset with an Azure Automation account to securely store them and reference them with your runbooks.</span></span>  <span data-ttu-id="75e88-120">Follow the steps in the section **To create a new credential** in the [Credential assets in Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) article and enter the following information:</span><span class="sxs-lookup"><span data-stu-id="75e88-120">Follow the steps in the section **To create a new credential** in the [Credential assets in Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) article and enter the following information:</span></span>

1. <span data-ttu-id="75e88-121">In the **Name** box, enter **AWScred** or an appropriate value following your naming standards.</span><span class="sxs-lookup"><span data-stu-id="75e88-121">In the **Name** box, enter **AWScred** or an appropriate value following your naming standards.</span></span>  
2. <span data-ttu-id="75e88-122">In the **User name** box type your **Access ID** and your **Secret Access Key** in the **Password** and **Confirm password** box.</span><span class="sxs-lookup"><span data-stu-id="75e88-122">In the **User name** box type your **Access ID** and your **Secret Access Key** in the **Password** and **Confirm password** box.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="75e88-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="75e88-123">Next steps</span></span>
* <span data-ttu-id="75e88-124">Reivew the solution article [Automating deployment of a VM in Amazon Web Services](automation-scenario-aws-deployment.md) to learn how to create runbooks to automate tasks in AWS.</span><span class="sxs-lookup"><span data-stu-id="75e88-124">Reivew the solution article [Automating deployment of a VM in Amazon Web Services](automation-scenario-aws-deployment.md) to learn how to create runbooks to automate tasks in AWS.</span></span>

