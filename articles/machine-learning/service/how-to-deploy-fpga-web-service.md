---
title: How to deploy a model as a web service on an FPGA with Azure Machine Learning
description: Learn how to deploy a web service with a model running on an FPGA with Azure Machine Learning.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: tedway
author: tedway
ms.date: 05/07/2018
ms.openlocfilehash: 85dcb224ad447b05fad6c18b075a5dcfc69a0b20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868029"
---
# <a name="deploy-a-model-as-a-web-service-on-an-fpga-with-azure-machine-learning"></a><span data-ttu-id="5e9e3-103">Deploy a model as a web service on an FPGA with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5e9e3-103">Deploy a model as a web service on an FPGA with Azure Machine Learning</span></span>

<span data-ttu-id="5e9e3-104">In this document, you learn how to set up your workstation environment and deploy a model as a web service on [field programmable gate arrays (FPGA)](concept-accelerate-with-fpgas.md).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-104">In this document, you learn how to set up your workstation environment and deploy a model as a web service on [field programmable gate arrays (FPGA)](concept-accelerate-with-fpgas.md).</span></span> <span data-ttu-id="5e9e3-105">The web service uses Project Brainwave to run the model on FPGA.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-105">The web service uses Project Brainwave to run the model on FPGA.</span></span>

<span data-ttu-id="5e9e3-106">Using FPGAs provides ultra-low latency inferencing, even with a single batch size.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-106">Using FPGAs provides ultra-low latency inferencing, even with a single batch size.</span></span>

## <a name="create-an-azure-machine-learning-model-management-account"></a><span data-ttu-id="5e9e3-107">Create an Azure Machine Learning Model Management account</span><span class="sxs-lookup"><span data-stu-id="5e9e3-107">Create an Azure Machine Learning Model Management account</span></span>

1. <span data-ttu-id="5e9e3-108">Go to the Model Management Account creation page on the [Azure Portal](https://aka.ms/aml-create-mma).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-108">Go to the Model Management Account creation page on the [Azure Portal](https://aka.ms/aml-create-mma).</span></span>

2. <span data-ttu-id="5e9e3-109">In the portal, create a Model Management Account in the **East US 2** region.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-109">In the portal, create a Model Management Account in the **East US 2** region.</span></span>

   ![Image of the Create Model Management Account screen](media/how-to-deploy-fpga-web-service/azure-portal-create-mma.PNG)

3. <span data-ttu-id="5e9e3-111">Give your Model Management Account a name, choose a subscription, and choose a resource group.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-111">Give your Model Management Account a name, choose a subscription, and choose a resource group.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="5e9e3-112">For Location, you MUST choose **East US 2** as the region.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-112">For Location, you MUST choose **East US 2** as the region.</span></span>  <span data-ttu-id="5e9e3-113">No other regions are currently available.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-113">No other regions are currently available.</span></span>

4. <span data-ttu-id="5e9e3-114">Choose a pricing tier (S1 is sufficient, but S2 and S3 also work).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-114">Choose a pricing tier (S1 is sufficient, but S2 and S3 also work).</span></span>  <span data-ttu-id="5e9e3-115">The DevTest tier is not supported.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-115">The DevTest tier is not supported.</span></span>  

5. <span data-ttu-id="5e9e3-116">Click **Select** to confirm the pricing tier.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-116">Click **Select** to confirm the pricing tier.</span></span>

6. <span data-ttu-id="5e9e3-117">Click **Create** on the ML Model Management on the left.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-117">Click **Create** on the ML Model Management on the left.</span></span>

## <a name="get-model-management-account-information"></a><span data-ttu-id="5e9e3-118">Get Model Management account information</span><span class="sxs-lookup"><span data-stu-id="5e9e3-118">Get Model Management account information</span></span>

<span data-ttu-id="5e9e3-119">To get information about your Model Management Account (MMA), click the __Model Management Account__ on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-119">To get information about your Model Management Account (MMA), click the __Model Management Account__ on the Azure portal.</span></span>

<span data-ttu-id="5e9e3-120">Copy the values of the following items:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-120">Copy the values of the following items:</span></span>

+ <span data-ttu-id="5e9e3-121">Model Management Account name (in on the upper left corner)</span><span class="sxs-lookup"><span data-stu-id="5e9e3-121">Model Management Account name (in on the upper left corner)</span></span>
+ <span data-ttu-id="5e9e3-122">Resource group name</span><span class="sxs-lookup"><span data-stu-id="5e9e3-122">Resource group name</span></span>
+ <span data-ttu-id="5e9e3-123">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="5e9e3-123">Subscription ID</span></span>
+ <span data-ttu-id="5e9e3-124">Location (use "eastus2")</span><span class="sxs-lookup"><span data-stu-id="5e9e3-124">Location (use "eastus2")</span></span>

![Model Management Account info](media/how-to-deploy-fpga-web-service/azure-portal-mma-info.PNG)

## <a name="set-up-your-machine"></a><span data-ttu-id="5e9e3-126">Set up your machine</span><span class="sxs-lookup"><span data-stu-id="5e9e3-126">Set up your machine</span></span>

<span data-ttu-id="5e9e3-127">To set up your workstation for FPGA deployment, use these steps:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-127">To set up your workstation for FPGA deployment, use these steps:</span></span>

1. <span data-ttu-id="5e9e3-128">Download and install the latest version of [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-128">Download and install the latest version of [Git](https://git-scm.com/downloads).</span></span>

2. <span data-ttu-id="5e9e3-129">Install [Anaconda (Python 3.6)](https://conda.io/miniconda.html).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-129">Install [Anaconda (Python 3.6)](https://conda.io/miniconda.html).</span></span>

3. <span data-ttu-id="5e9e3-130">To download the Anaconda environment, use the following command from a Git prompt:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-130">To download the Anaconda environment, use the following command from a Git prompt:</span></span>

    ```
    git clone https://aka.ms/aml-real-time-ai
    ```

4. <span data-ttu-id="5e9e3-131">To create the environment, open an **Anaconda Prompt** (not an Azure Machine Learning Workbench prompt) and run the following command:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-131">To create the environment, open an **Anaconda Prompt** (not an Azure Machine Learning Workbench prompt) and run the following command:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5e9e3-132">The `environment.yml` file is in the git repository you cloned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-132">The `environment.yml` file is in the git repository you cloned in the previous step.</span></span> <span data-ttu-id="5e9e3-133">Change the path as needed to point to the file on your workstation.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-133">Change the path as needed to point to the file on your workstation.</span></span>

    ```
    conda env create -f environment.yml
    ```

5. <span data-ttu-id="5e9e3-134">To activate the environment, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-134">To activate the environment, use the following command:</span></span>

    ```
    conda activate amlrealtimeai
    ```

6. <span data-ttu-id="5e9e3-135">To start the Jupyter Notebook server, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-135">To start the Jupyter Notebook server, use the following command:</span></span>

    ```
    jupyter notebook
    ```

    <span data-ttu-id="5e9e3-136">The output of this command is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-136">The output of this command is similar to the following text:</span></span>

    ```text
    Copy/paste this URL into your browser when you connect for the first time, to login with a token:
        http://localhost:8888/?token=bb2ce89cc8ae931f5df50f96e3a6badfc826ff4100e78075
    ```

    > [!TIP]
    > <span data-ttu-id="5e9e3-137">You will get a different token each time you run the command.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-137">You will get a different token each time you run the command.</span></span>

    <span data-ttu-id="5e9e3-138">If your browser does not automatically open to the Jupyter notebook, use the HTTP URL returned by the previous command to open the page.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-138">If your browser does not automatically open to the Jupyter notebook, use the HTTP URL returned by the previous command to open the page.</span></span>

    ![Image of the Jupyter Notebook web page](./media/how-to-deploy-fpga-web-service/jupyter-notebook.png)

## <a name="deploy-your-model"></a><span data-ttu-id="5e9e3-140">Deploy your model</span><span class="sxs-lookup"><span data-stu-id="5e9e3-140">Deploy your model</span></span>

<span data-ttu-id="5e9e3-141">From the Jupyter Notebook, open the `00_QuickStart.ipynb` notebook from the `notebooks/resnet50` directory.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-141">From the Jupyter Notebook, open the `00_QuickStart.ipynb` notebook from the `notebooks/resnet50` directory.</span></span> <span data-ttu-id="5e9e3-142">Follow the instructions in the notebook to:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-142">Follow the instructions in the notebook to:</span></span>

* <span data-ttu-id="5e9e3-143">Define the service</span><span class="sxs-lookup"><span data-stu-id="5e9e3-143">Define the service</span></span>
* <span data-ttu-id="5e9e3-144">Deploy the model</span><span class="sxs-lookup"><span data-stu-id="5e9e3-144">Deploy the model</span></span>
* <span data-ttu-id="5e9e3-145">Consume the deployed model</span><span class="sxs-lookup"><span data-stu-id="5e9e3-145">Consume the deployed model</span></span>
* <span data-ttu-id="5e9e3-146">Delete deployed services</span><span class="sxs-lookup"><span data-stu-id="5e9e3-146">Delete deployed services</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e9e3-147">To optimize latency and throughput, your workstation should be in the same Azure region as the endpoint.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-147">To optimize latency and throughput, your workstation should be in the same Azure region as the endpoint.</span></span>  <span data-ttu-id="5e9e3-148">Currently the APIs are created in the East US Azure region.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-148">Currently the APIs are created in the East US Azure region.</span></span>

## <a name="ssltls-and-authentication"></a><span data-ttu-id="5e9e3-149">SSL/TLS and authentication</span><span class="sxs-lookup"><span data-stu-id="5e9e3-149">SSL/TLS and authentication</span></span>

<span data-ttu-id="5e9e3-150">Azure Machine Learning provides SSL support and key-based authentication.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-150">Azure Machine Learning provides SSL support and key-based authentication.</span></span> <span data-ttu-id="5e9e3-151">This enables you to restrict access to your service and secure data submitted by clients.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-151">This enables you to restrict access to your service and secure data submitted by clients.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9e3-152">The steps in this section only apply to Azure Machine Learning Hardware Accelerated Models.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-152">The steps in this section only apply to Azure Machine Learning Hardware Accelerated Models.</span></span> <span data-ttu-id="5e9e3-153">For standard Azure Machine Learning services, see the [How to set up SSL on Azure Machine Learning Compute](https://docs.microsoft.com/azure/machine-learning/preview/how-to-setup-ssl-on-mlc) document.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-153">For standard Azure Machine Learning services, see the [How to set up SSL on Azure Machine Learning Compute](https://docs.microsoft.com/azure/machine-learning/preview/how-to-setup-ssl-on-mlc) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e9e3-154">Authentication is only enabled for services that have provided an SSL certificate and key.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-154">Authentication is only enabled for services that have provided an SSL certificate and key.</span></span> 
>
> <span data-ttu-id="5e9e3-155">If you do not enable SSL, any user on the internet will be able to make calls to the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-155">If you do not enable SSL, any user on the internet will be able to make calls to the service.</span></span>
>
> <span data-ttu-id="5e9e3-156">If you enable SSL, and authentication key is required when accessing the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-156">If you enable SSL, and authentication key is required when accessing the service.</span></span>

<span data-ttu-id="5e9e3-157">SSL encrypts data sent between the client and the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-157">SSL encrypts data sent between the client and the service.</span></span> <span data-ttu-id="5e9e3-158">It also used by the client to verify the identity of the server.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-158">It also used by the client to verify the identity of the server.</span></span>

<span data-ttu-id="5e9e3-159">You can deploy a service with SSL enabled, or update an already deployed service to enable it.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-159">You can deploy a service with SSL enabled, or update an already deployed service to enable it.</span></span> <span data-ttu-id="5e9e3-160">The steps are the same:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-160">The steps are the same:</span></span>

1. <span data-ttu-id="5e9e3-161">Acquire a domain name.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-161">Acquire a domain name.</span></span>

2. <span data-ttu-id="5e9e3-162">Acquire an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-162">Acquire an SSL certificate.</span></span>

3. <span data-ttu-id="5e9e3-163">Deploy or update the service with SSL enabled.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-163">Deploy or update the service with SSL enabled.</span></span>

4. <span data-ttu-id="5e9e3-164">Update your DNS to point to the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-164">Update your DNS to point to the service.</span></span>

### <a name="acquire-a-domain-name"></a><span data-ttu-id="5e9e3-165">Acquire a domain name</span><span class="sxs-lookup"><span data-stu-id="5e9e3-165">Acquire a domain name</span></span>

<span data-ttu-id="5e9e3-166">If you do not already own a domain name, you can purchase one from a __domain name registrar__.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-166">If you do not already own a domain name, you can purchase one from a __domain name registrar__.</span></span> <span data-ttu-id="5e9e3-167">The process differs between registrars, as does the cost.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-167">The process differs between registrars, as does the cost.</span></span> <span data-ttu-id="5e9e3-168">The registrar also provides you with tools for managing the domain name.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-168">The registrar also provides you with tools for managing the domain name.</span></span> <span data-ttu-id="5e9e3-169">These tools are used to map a fully qualified domain name (such as www.contoso.com) to the IP address that your service is hosted at.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-169">These tools are used to map a fully qualified domain name (such as www.contoso.com) to the IP address that your service is hosted at.</span></span>

### <a name="acquire-an-ssl-certificate"></a><span data-ttu-id="5e9e3-170">Acquire an SSL certificate</span><span class="sxs-lookup"><span data-stu-id="5e9e3-170">Acquire an SSL certificate</span></span>

<span data-ttu-id="5e9e3-171">There are many ways to get an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-171">There are many ways to get an SSL certificate.</span></span> <span data-ttu-id="5e9e3-172">The most common is to purchase one from a __Certificate Authority__ (CA).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-172">The most common is to purchase one from a __Certificate Authority__ (CA).</span></span> <span data-ttu-id="5e9e3-173">Regardless of where you obtain the certificate, you need the following files:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-173">Regardless of where you obtain the certificate, you need the following files:</span></span>

* <span data-ttu-id="5e9e3-174">A __certificate__.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-174">A __certificate__.</span></span> <span data-ttu-id="5e9e3-175">The certificate must contain the full certificate chain, and must be PEM-encoded.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-175">The certificate must contain the full certificate chain, and must be PEM-encoded.</span></span>
* <span data-ttu-id="5e9e3-176">A __key__.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-176">A __key__.</span></span> <span data-ttu-id="5e9e3-177">The key must be PEM-encoded.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-177">The key must be PEM-encoded.</span></span>

> [!TIP]
> <span data-ttu-id="5e9e3-178">If the Certificate Authority cannot provide the certificate and key as PEM-encoded files, you can use a utility such as [OpenSSL](https://www.openssl.org/) to change the format.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-178">If the Certificate Authority cannot provide the certificate and key as PEM-encoded files, you can use a utility such as [OpenSSL](https://www.openssl.org/) to change the format.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e9e3-179">Self-signed certificates should be used only for development.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-179">Self-signed certificates should be used only for development.</span></span> <span data-ttu-id="5e9e3-180">They should not be used in production.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-180">They should not be used in production.</span></span>
>
> <span data-ttu-id="5e9e3-181">If you use a self-signed certificate, see the [Consuming services with self-signed certificates](#self-signed) section for specific instructions.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-181">If you use a self-signed certificate, see the [Consuming services with self-signed certificates](#self-signed) section for specific instructions.</span></span>

> [!WARNING]
> <span data-ttu-id="5e9e3-182">When requesting a certificate, you must provide the fully qualified domain name (FQDN) of the address you plan to use for the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-182">When requesting a certificate, you must provide the fully qualified domain name (FQDN) of the address you plan to use for the service.</span></span> <span data-ttu-id="5e9e3-183">For example, www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-183">For example, www.contoso.com.</span></span> <span data-ttu-id="5e9e3-184">The address stamped into the certificate and the address used by the clients are compared when validating the identity of the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-184">The address stamped into the certificate and the address used by the clients are compared when validating the identity of the service.</span></span>
>
> <span data-ttu-id="5e9e3-185">If the addresses do not match, the clients will receive an error.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-185">If the addresses do not match, the clients will receive an error.</span></span> 

### <a name="deploy-or-update-the-service-with-ssl-enabled"></a><span data-ttu-id="5e9e3-186">Deploy or update the service with SSL enabled</span><span class="sxs-lookup"><span data-stu-id="5e9e3-186">Deploy or update the service with SSL enabled</span></span>

<span data-ttu-id="5e9e3-187">To deploy the service with SSL enabled, set the `ssl_enabled` parameter to `True`.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-187">To deploy the service with SSL enabled, set the `ssl_enabled` parameter to `True`.</span></span> <span data-ttu-id="5e9e3-188">Set the `ssl_certificate` parameter to the value of the __certificate__ file and the `ssl_key` to the value of the __key__ file.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-188">Set the `ssl_certificate` parameter to the value of the __certificate__ file and the `ssl_key` to the value of the __key__ file.</span></span> <span data-ttu-id="5e9e3-189">The following example demonstrates deploying a service with SSL enabled:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-189">The following example demonstrates deploying a service with SSL enabled:</span></span>

```python
from amlrealtimeai import DeploymentClient

subscription_id = "<Your Azure Subscription ID>"
resource_group = "<Your Azure Resource Group Name>"
model_management_account = "<Your AzureML Model Management Account Name>"
location = "eastus2"

model_name = "resnet50-model"
service_name = "quickstart-service"

deployment_client = DeploymentClient(subscription_id, resource_group, model_management_account, location)

with open('cert.pem','r') as cert_file:
    with open('key.pem','r') as key_file:
        cert = cert_file.read()
        key = key_file.read()
        service = deployment_client.create_service(service_name, model_id, ssl_enabled=True, ssl_certificate=cert, ssl_key=key)
```

<span data-ttu-id="5e9e3-190">The response of the `create_service` operation contains the IP address of the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-190">The response of the `create_service` operation contains the IP address of the service.</span></span> <span data-ttu-id="5e9e3-191">The IP address is used when mapping the DNS name to the IP address of the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-191">The IP address is used when mapping the DNS name to the IP address of the service.</span></span>

<span data-ttu-id="5e9e3-192">The response also contains a __primary key__ and __secondary key__ that are used to consume the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-192">The response also contains a __primary key__ and __secondary key__ that are used to consume the service.</span></span>

### <a name="update-your-dns-to-point-to-the-service"></a><span data-ttu-id="5e9e3-193">Update your DNS to point to the service</span><span class="sxs-lookup"><span data-stu-id="5e9e3-193">Update your DNS to point to the service</span></span>

<span data-ttu-id="5e9e3-194">Use the tools provided by your domain name registrar to update the DNS record for your domain name.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-194">Use the tools provided by your domain name registrar to update the DNS record for your domain name.</span></span> <span data-ttu-id="5e9e3-195">The record must point to the IP address of the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-195">The record must point to the IP address of the service.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9e3-196">Depending on the registrar, and the time to live (TTL) configured for the domain name, it can take several minutes to several hours before clients can resolve the domain name.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-196">Depending on the registrar, and the time to live (TTL) configured for the domain name, it can take several minutes to several hours before clients can resolve the domain name.</span></span>

### <a name="consuming-authenticated-services"></a><span data-ttu-id="5e9e3-197">Consuming authenticated services</span><span class="sxs-lookup"><span data-stu-id="5e9e3-197">Consuming authenticated services</span></span>

<span data-ttu-id="5e9e3-198">The following examples demonstrate how to consume an authenticated service using Python and C#:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-198">The following examples demonstrate how to consume an authenticated service using Python and C#:</span></span>

> [!NOTE]
> <span data-ttu-id="5e9e3-199">Replace `authkey` with the primary or secondary key returned when creating the service.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-199">Replace `authkey` with the primary or secondary key returned when creating the service.</span></span>

```python
from amlrealtimeai import PredictionClient
client = PredictionClient(service.ipAddress, service.port, use_ssl=True, access_token="authKey")
image_file = R'C:\path_to_file\image.jpg'
results = client.score_image(image_file)
```

```csharp
var client = new ScoringClient(host, 50051, useSSL, "authKey");
float[,] result;
using (var content = File.OpenRead(image))
    {
        IScoringRequest request = new ImageRequest(content);
        result = client.Score<float[,]>(request);
    }
```

<span data-ttu-id="5e9e3-200">Other gRPC clients can authenticate requests by setting an authorization header.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-200">Other gRPC clients can authenticate requests by setting an authorization header.</span></span> <span data-ttu-id="5e9e3-201">The general approach is to create a `ChannelCredentials` object that combines `SslCredentials` with `CallCredentials`.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-201">The general approach is to create a `ChannelCredentials` object that combines `SslCredentials` with `CallCredentials`.</span></span> <span data-ttu-id="5e9e3-202">This is added to the authorization header of the request.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-202">This is added to the authorization header of the request.</span></span> <span data-ttu-id="5e9e3-203">For more information on implementing support for your specific headers, see [https://grpc.io/docs/guides/auth.html](https://grpc.io/docs/guides/auth.html).</span><span class="sxs-lookup"><span data-stu-id="5e9e3-203">For more information on implementing support for your specific headers, see [https://grpc.io/docs/guides/auth.html](https://grpc.io/docs/guides/auth.html).</span></span>

<span data-ttu-id="5e9e3-204">The following examples demonstrate how to set the header in C# and Go:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-204">The following examples demonstrate how to set the header in C# and Go:</span></span>

```csharp
creds = ChannelCredentials.Create(baseCreds, CallCredentials.FromInterceptor(
                      async (context, metadata) =>
                      {
                          metadata.Add(new Metadata.Entry("authorization", "authKey"));
                          await Task.CompletedTask;
                      }));

```

```go
conn, err := grpc.Dial(serverAddr, 
    grpc.WithTransportCredentials(credentials.NewClientTLSFromCert(nil, "")),
    grpc.WithPerRPCCredentials(&authCreds{
    Key: "authKey"}))

type authCreds struct {
    Key string
}

func (c *authCreds) GetRequestMetadata(context.Context, uri ...string) (map[string]string, error) {
    return map[string]string{
        "authorization": c.Key,
    }, nil
}

func (c *authCreds) RequireTransportSecurity() bool {
    return true
}
```

### <a id="self-signed"></a><span data-ttu-id="5e9e3-205">Consuming services with self-signed certificates</span><span class="sxs-lookup"><span data-stu-id="5e9e3-205">Consuming services with self-signed certificates</span></span>

<span data-ttu-id="5e9e3-206">There are two ways to enable the client to authenticate to a server secured with a self-signed certificate:</span><span class="sxs-lookup"><span data-stu-id="5e9e3-206">There are two ways to enable the client to authenticate to a server secured with a self-signed certificate:</span></span>

* <span data-ttu-id="5e9e3-207">On the client system, set the `GRPC_DEFAULT_SSL_ROOTS_FILE_PATH` environment variable on the client system to point to the certificate file.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-207">On the client system, set the `GRPC_DEFAULT_SSL_ROOTS_FILE_PATH` environment variable on the client system to point to the certificate file.</span></span>

* <span data-ttu-id="5e9e3-208">When constructing an `SslCredentials` object, pass the contents of the certificate file to the constructor.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-208">When constructing an `SslCredentials` object, pass the contents of the certificate file to the constructor.</span></span>

<span data-ttu-id="5e9e3-209">Using either method causes gRPC to use the certificate as the root cert.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-209">Using either method causes gRPC to use the certificate as the root cert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e9e3-210">gRPC will not accept untrusted certificates.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-210">gRPC will not accept untrusted certificates.</span></span> <span data-ttu-id="5e9e3-211">Using an untrusted certificate will fail with an `Unavailable` status code.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-211">Using an untrusted certificate will fail with an `Unavailable` status code.</span></span> <span data-ttu-id="5e9e3-212">The details of the failure contain `Connection Failed`.</span><span class="sxs-lookup"><span data-stu-id="5e9e3-212">The details of the failure contain `Connection Failed`.</span></span>
