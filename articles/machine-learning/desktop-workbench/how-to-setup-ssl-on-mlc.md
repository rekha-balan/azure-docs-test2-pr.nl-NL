---
title: Enable SSL on an Azure Machine Learning Compute (MLC) cluster | Microsoft Docs
description: Get instructions for setting up SSL for scoring calls on an Azure Machine Learning Compute (MLC) cluster
services: machine-learning
author: SerinaKaye
ms.author: serinak
manager: hjerez
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 01/24/2018
ms.openlocfilehash: 011ee428cc2614c3d97b4b060f212b6bdc0416b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867178"
---
# <a name="enable-ssl-on-an-azure-machine-learning-compute-mlc-cluster"></a><span data-ttu-id="d20b0-103">Enable SSL on an Azure Machine Learning Compute (MLC) cluster</span><span class="sxs-lookup"><span data-stu-id="d20b0-103">Enable SSL on an Azure Machine Learning Compute (MLC) cluster</span></span> 

<span data-ttu-id="d20b0-104">These instructions allow you to set up SSL for scoring calls on a Machine Learning Compute (MLC) cluster.</span><span class="sxs-lookup"><span data-stu-id="d20b0-104">These instructions allow you to set up SSL for scoring calls on a Machine Learning Compute (MLC) cluster.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d20b0-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d20b0-105">Prerequisites</span></span> 

1. <span data-ttu-id="d20b0-106">Decide on a CNAME (DNS name) to use when making real-time scoring calls.</span><span class="sxs-lookup"><span data-stu-id="d20b0-106">Decide on a CNAME (DNS name) to use when making real-time scoring calls.</span></span>

2. <span data-ttu-id="d20b0-107">Create a *password-free* certificate with that CNAME.</span><span class="sxs-lookup"><span data-stu-id="d20b0-107">Create a *password-free* certificate with that CNAME.</span></span>

3. <span data-ttu-id="d20b0-108">If the certificate is not already in PEM format, convert it to PEM using tools such as *openssl*.</span><span class="sxs-lookup"><span data-stu-id="d20b0-108">If the certificate is not already in PEM format, convert it to PEM using tools such as *openssl*.</span></span>

<span data-ttu-id="d20b0-109">You will have two files after completing the prerequisites:</span><span class="sxs-lookup"><span data-stu-id="d20b0-109">You will have two files after completing the prerequisites:</span></span>

* <span data-ttu-id="d20b0-110">A file for the certificate, for example, `cert.pem`.</span><span class="sxs-lookup"><span data-stu-id="d20b0-110">A file for the certificate, for example, `cert.pem`.</span></span> <span data-ttu-id="d20b0-111">Make sure the file has the full certificate chain.</span><span class="sxs-lookup"><span data-stu-id="d20b0-111">Make sure the file has the full certificate chain.</span></span>
* <span data-ttu-id="d20b0-112">A file for the key, for example, `key.pem`</span><span class="sxs-lookup"><span data-stu-id="d20b0-112">A file for the key, for example, `key.pem`</span></span>



## <a name="set-up-an-ssl-certificate-on-a-new-acs-cluster"></a><span data-ttu-id="d20b0-113">Set up an SSL certificate on a new ACS cluster</span><span class="sxs-lookup"><span data-stu-id="d20b0-113">Set up an SSL certificate on a new ACS cluster</span></span>

<span data-ttu-id="d20b0-114">Using the Azure Machine Learning CLI, run the following command with the `-c` switch to create an ACS cluster with an SSL certificate attached:</span><span class="sxs-lookup"><span data-stu-id="d20b0-114">Using the Azure Machine Learning CLI, run the following command with the `-c` switch to create an ACS cluster with an SSL certificate attached:</span></span>

```
az ml env create -c -g <resource group name> -n <cluster name> --cert-cname <CNAME> --cert-pem <path to cert.pem file> --key-pem <path to key.pem file>
```


## <a name="set-up-an-ssl-certificate-on-an-existing-acs-cluster"></a><span data-ttu-id="d20b0-115">Set up an SSL certificate on an existing ACS cluster</span><span class="sxs-lookup"><span data-stu-id="d20b0-115">Set up an SSL certificate on an existing ACS cluster</span></span>

<span data-ttu-id="d20b0-116">If you are targeting a cluster that was created without SSL, you can add a certificate using Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d20b0-116">If you are targeting a cluster that was created without SSL, you can add a certificate using Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="d20b0-117">You need to provide the key and certificate in raw PEM format.</span><span class="sxs-lookup"><span data-stu-id="d20b0-117">You need to provide the key and certificate in raw PEM format.</span></span> <span data-ttu-id="d20b0-118">These can be read into PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="d20b0-118">These can be read into PowerShell variables:</span></span>

```
$keyValueInPemFormat = [IO.File]::ReadAllText('<path to key.pem file>')
$certValueInPemFormat = [IO.File]::ReadAllText('<path to cert.pem file>')
```
<span data-ttu-id="d20b0-119">Add the certificate to the cluster:</span><span class="sxs-lookup"><span data-stu-id="d20b0-119">Add the certificate to the cluster:</span></span> 

```
Set-AzureRmMlOpCluster -ResourceGroupName my-rg -Name my-cluster -SslStatus Enabled -SslCertificate $certValueInPemFormat -SslKey $keyValueInPemFormat -SslCName foo.mycompany.com
```

## <a name="map-the-cname-and-the-ip-address"></a><span data-ttu-id="d20b0-120">Map the CNAME and the IP Address</span><span class="sxs-lookup"><span data-stu-id="d20b0-120">Map the CNAME and the IP Address</span></span>

<span data-ttu-id="d20b0-121">Create a mapping between the CNAME you selected in the prerequisites and the IP address of the real-time front-end (FE).</span><span class="sxs-lookup"><span data-stu-id="d20b0-121">Create a mapping between the CNAME you selected in the prerequisites and the IP address of the real-time front-end (FE).</span></span> <span data-ttu-id="d20b0-122">To discover the IP address of the FE, run the command below.</span><span class="sxs-lookup"><span data-stu-id="d20b0-122">To discover the IP address of the FE, run the command below.</span></span> <span data-ttu-id="d20b0-123">The output displays a field called "publicIpAddress" which contains the IP address of the real-time cluster front-end.</span><span class="sxs-lookup"><span data-stu-id="d20b0-123">The output displays a field called "publicIpAddress" which contains the IP address of the real-time cluster front-end.</span></span> <span data-ttu-id="d20b0-124">Refer to the instructions of your DNS provider to set up a record from the FQDN used in CNAME to the public IP address.</span><span class="sxs-lookup"><span data-stu-id="d20b0-124">Refer to the instructions of your DNS provider to set up a record from the FQDN used in CNAME to the public IP address.</span></span>



## <a name="auto-detection-of-a-certificate"></a><span data-ttu-id="d20b0-125">Auto-detection of a certificate</span><span class="sxs-lookup"><span data-stu-id="d20b0-125">Auto-detection of a certificate</span></span> 

<span data-ttu-id="d20b0-126">When you create a real-time web service using the "`az ml service create realtime`" command, Azure Machine Learning auto-detects the SSL set up on the cluster and automatically sets up the scoring URL with the designated certificate.</span><span class="sxs-lookup"><span data-stu-id="d20b0-126">When you create a real-time web service using the "`az ml service create realtime`" command, Azure Machine Learning auto-detects the SSL set up on the cluster and automatically sets up the scoring URL with the designated certificate.</span></span> 

<span data-ttu-id="d20b0-127">To see the certificate status, run the following command.</span><span class="sxs-lookup"><span data-stu-id="d20b0-127">To see the certificate status, run the following command.</span></span> <span data-ttu-id="d20b0-128">Notice the "https" prefix of the scoring URI and the CNAME in the host name.</span><span class="sxs-lookup"><span data-stu-id="d20b0-128">Notice the "https" prefix of the scoring URI and the CNAME in the host name.</span></span> 

``` 
az ml service show realtime -n <service name>
{
                "id" : "<your service id>",
                "name" : "<your service name >",
                "state" : "Succeeded",
                "createdAt" : "<datetime>”,
                "updatedAt" : "< datetime>",
                "scoringUri" : "https://<your CNAME>/api/v1/service/<service name>/score"
}
```
