---
title: Azure Machine Learning Model Management command-line interface reference | Microsoft Docs
description: Azure Machine Learning Model Management command-line interface reference.
services: machine-learning
author: aashishb
ms.author: aashishb
manager: hjerez
ms.reviewer: jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 11/08/2017
ms.openlocfilehash: 9e69f2e71cce6d689669838785ce992fbbcfa940
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870549"
---
# <a name="model-management-command-line-interface-reference"></a><span data-ttu-id="a4ef8-103">Model management command-line interface reference</span><span class="sxs-lookup"><span data-stu-id="a4ef8-103">Model management command-line interface reference</span></span>

## <a name="base-cli-concepts"></a><span data-ttu-id="a4ef8-104">Base CLI concepts:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-104">Base CLI concepts:</span></span>

    account : Manage model management accounts. 
    env     : Manage compute environments.
    image   : Manage operationalization images.
    manifest: Manage operationalization manifests.
    model   : Manage operationalization models.
    service : Manage operationalized services.

## <a name="account-commands"></a><span data-ttu-id="a4ef8-105">Account commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-105">Account commands</span></span>
<span data-ttu-id="a4ef8-106">A model management account is required to use the services, which allow you to deploy and manage models.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-106">A model management account is required to use the services, which allow you to deploy and manage models.</span></span> <span data-ttu-id="a4ef8-107">Use `az ml account modelmanagement -h` to see the following list:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-107">Use `az ml account modelmanagement -h` to see the following list:</span></span>

    create: Create a Model Management Account.
    delete: Delete a specified Model Management Account.
    list  : Gets the Model Management Accounts in the current subscriptiong.
    set   : Set the active Model Management Account.
    show  : Show a Model Management Account.
    update: Update an existing Model Management Account.

<span data-ttu-id="a4ef8-108">**Create Model Management Account**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-108">**Create Model Management Account**</span></span>

<span data-ttu-id="a4ef8-109">Create a model management account for billing using the following command:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-109">Create a model management account for billing using the following command:</span></span>

`az ml account modelmanagement create --location [Azure region e.g. eastus2] --name [new account name] --resource-group [resource group name to store the account in]`

<span data-ttu-id="a4ef8-110">Local Arguments:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-110">Local Arguments:</span></span>

    --location -l       [Required]: Resource location.
    --name -n           [Required]: Name of the model management account.
    --resource-group -g [Required]: Resource group to create the model management account in.
    --description -d              : Description of the model management account.
    --sku-instances               : Number of instances of the selected SKU. Must be between 1 and
                                    16 inclusive.  Default: 1.
    --sku-name                    : SKU name. Valid names are S1|S2|S3|DevTest.  Default: S1.
    --tags -t                     : Tags for the model management account.  Default: {}.
    -v                            : Verbosity flag.

## <a name="environment-commands"></a><span data-ttu-id="a4ef8-111">Environment commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-111">Environment commands</span></span>

    cluster        : Switch the current execution context to 'cluster'.
    delete         : Delete an MLCRP-provisioned resource.
    get-credentials: List the keys for an environment.
    list           : List all environments in the current subscription.
    local          : Switch the current execution context to 'local'.
    set            : Set the active MLC environment.
    setup          : Sets up an MLC environment.
    show           : Show an MLC resource; if resource_group or cluster_name are not provided, shows
                     the active MLC env.

<span data-ttu-id="a4ef8-112">**Set up the Deployment Environment**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-112">**Set up the Deployment Environment**</span></span>

<span data-ttu-id="a4ef8-113">The setup command requires you to have Contributor access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-113">The setup command requires you to have Contributor access to the subscription.</span></span> <span data-ttu-id="a4ef8-114">If you don't have that, you at least need Contributor access to the resource group that you are deploying into.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-114">If you don't have that, you at least need Contributor access to the resource group that you are deploying into.</span></span> <span data-ttu-id="a4ef8-115">To do the latter, you need to specify the resource group name as part of the setup command using `-g` the flag.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-115">To do the latter, you need to specify the resource group name as part of the setup command using `-g` the flag.</span></span> 

<span data-ttu-id="a4ef8-116">There are two options for deployment: *local* and *cluster*.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-116">There are two options for deployment: *local* and *cluster*.</span></span> <span data-ttu-id="a4ef8-117">Setting the `--cluster` (or `-c`) flag enables cluster deployment, which provisions an ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-117">Setting the `--cluster` (or `-c`) flag enables cluster deployment, which provisions an ACS cluster.</span></span> <span data-ttu-id="a4ef8-118">The basic setup syntax is as follows:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-118">The basic setup syntax is as follows:</span></span>

`az ml env setup [-c] --location [location of environment resources] --name[name of environment]`

<span data-ttu-id="a4ef8-119">This command initializes your Azure machine learning environment with a storage account, ACR registry, and App Insights service created in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-119">This command initializes your Azure machine learning environment with a storage account, ACR registry, and App Insights service created in your subscription.</span></span> <span data-ttu-id="a4ef8-120">By default, the environment is initialized for local deployments only (no ACS) if no flag is specified.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-120">By default, the environment is initialized for local deployments only (no ACS) if no flag is specified.</span></span> <span data-ttu-id="a4ef8-121">If you need to scale service, specify the `--cluster` (or `-c`) flag to create an ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-121">If you need to scale service, specify the `--cluster` (or `-c`) flag to create an ACS cluster.</span></span>

<span data-ttu-id="a4ef8-122">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-122">Command details:</span></span>

    --location -l        [Required]: Location for environment resources; an Azure region, e.g. eastus2.
    --name -n            [Required]: Name of environment to provision.
    --acr -r                       : ARM ID of ACR to associate with this environment.
    --agent-count -z               : Number of agents to provision in the ACS cluster. Default: 3.
    --cert-cname                   : CNAME of certificate.
    --cert-pem                     : Path to .pem file with certificate bytes.
    --cluster -c                   : Flag to provision ACS cluster. Off by default; specify this to force an ACS cluster deployment.
    --key-pem                      : Path to .pem file with certificate key.
    --master-count -m              : Number of master nodes to provision in the ACS cluster. Acceptable values: 1, 3, 5. Default: 1.
    --resource-group -g            : Resource group in which to create compute resource. Is created if it does not exist.
                                     If not provided, resource group is created with 'rg' appended to 'name.'.
    --service-principal-app-id -a  : App ID of service principal to use for configuring ML compute.
    --service-principal-password -p: Password associated with service principal.
    --storage -s                   : ARM ID of storage account to associate with this environment.
    --yes -y                       : Flag to answer 'yes' to any prompts. Command fails if user is not logged in.

<span data-ttu-id="a4ef8-123">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-123">Global Arguments</span></span>
```
    --debug                        : Increase logging verbosity to show all debug logs.
    --help -h                      : Show this help message and exit.
    --output -o                    : Output format.  Allowed values: json, jsonc, table, tsv. Default: json.
    --query                        : JMESPath query string. See http://jmespath.org/ for more information and examples.
    --verbose                      : Increase logging verbosity. Use --debug for full debug logs.
```
## <a name="model-commands"></a><span data-ttu-id="a4ef8-124">Model commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-124">Model commands</span></span>

    list
    register
    show

<span data-ttu-id="a4ef8-125">**Register a model**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-125">**Register a model**</span></span>

<span data-ttu-id="a4ef8-126">Command to register the model.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-126">Command to register the model.</span></span>

`az ml model register --model [path to model file] --name [model name]`

<span data-ttu-id="a4ef8-127">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-127">Command details:</span></span>

    --model -m [Required]: Model to register.
    --name -n  [Required]: Name of model to register.
    --description -d     : Description of the model.
    --tag -t             : Tags for the model. Multiple tags can be specified with additional -t arguments.
    -v                   : Verbosity flag.

<span data-ttu-id="a4ef8-128">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-128">Global Arguments</span></span>

    --debug              : Increase logging verbosity to show all debug logs.
    --help -h            : Show this help message and exit.
    --output -o          : Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
    --query              : JMESPath query string. See http://jmespath.org/ for more information and
                           examples.
    --verbose            : Increase logging verbosity. Use --debug for full debug logs.

## <a name="manifest-commands"></a><span data-ttu-id="a4ef8-129">Manifest commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-129">Manifest commands</span></span>

    create: Create an Operationalization Manifest. This command has two different
            sets of required arguments, depending on if you want to use previously registered
            model/s.
    list
    show

<span data-ttu-id="a4ef8-130">**Create manifest**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-130">**Create manifest**</span></span>

<span data-ttu-id="a4ef8-131">The following command creates a manifest file for the model.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-131">The following command creates a manifest file for the model.</span></span> 

`az ml manifest create --manifest-name [your new manifest name] -f [path to code file] -r [runtime for the image, e.g. spark-py]`

<span data-ttu-id="a4ef8-132">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-132">Command details:</span></span>

    --manifest-name -n [Required]: Name of the manifest to create.
    -f                 [Required]: The code file to be deployed.
    -r                 [Required]: Runtime of the web service. Valid runtimes are spark-py|python.
    --conda-file -c              : Path to Conda Environment file.
    --dependency -d              : Files and directories required by the service. Multiple
                                   dependencies can be specified with additional -d arguments.
    --manifest-description       : Description of the manifest.
    --schema-file -s             : Schema file to add to the manifest.
    -p                           : A pip requirements.txt file needed by the code file.
    -v                           : Verbosity flag.

<span data-ttu-id="a4ef8-133">Registered Model Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-133">Registered Model Arguments</span></span>

    --model-id -i                : [Required] Id of previously registered model to add to manifest.
                                   Multiple models can be specified with additional -i arguments.

<span data-ttu-id="a4ef8-134">Unregistered Model Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-134">Unregistered Model Arguments</span></span>

    --model-file -m              : [Required] Model file to register. If used, must be combined with
                                   model name.

<span data-ttu-id="a4ef8-135">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-135">Global Arguments</span></span>

    --debug                      : Increase logging verbosity to show all debug logs.
    --help -h                    : Show this help message and exit.
    --output -o                  : Output format.  Allowed values: json, jsonc, table, tsv.
                                   Default: json.
    --query                      : JMESPath query string. See http://jmespath.org/ for more
                                   information and examples.
    --verbose                    : Increase logging verbosity. Use --debug for full debug logs.


## <a name="image-commands"></a><span data-ttu-id="a4ef8-136">Image commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-136">Image commands</span></span>

    create: Creates a docker image with the model and its dependencies. This command has two different sets of
            required arguments, depending on if you want to use a previously created manifest.
    list
    show
    usage

<span data-ttu-id="a4ef8-137">**Create image**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-137">**Create image**</span></span>

<span data-ttu-id="a4ef8-138">You can create an image with the option of having created its manifest before.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-138">You can create an image with the option of having created its manifest before.</span></span> 

`az ml image create -n [image name] --manifest-id [the manifest ID]`

<span data-ttu-id="a4ef8-139">Or you can create the manifest and image with a single command.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-139">Or you can create the manifest and image with a single command.</span></span> 

`az ml image create -n [image name] --model-file [model file or folder path] -f [code file, e.g. the score.py file] -r [the runtime eg.g. spark-py which is the Docker container image base]`

<span data-ttu-id="a4ef8-140">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-140">Command details:</span></span>

    --image-name -n [Required]: The name of the image being created.
    --image-description       : Description of the image.
    --image-type              : The image type to create. Defaults to "Docker".
    -v                        : Verbosity flag.

<span data-ttu-id="a4ef8-141">Registered Manifest Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-141">Registered Manifest Arguments</span></span>

    --manifest-id             : [Required] Id of previously registered manifest to use in image creation.

<span data-ttu-id="a4ef8-142">Unregistered Manifest Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-142">Unregistered Manifest Arguments</span></span>

    --conda-file -c           : Path to Conda Environment file.
    --dependency -d           : Files and directories required by the service. Multiple dependencies can
                                be specified with additional -d arguments.
    --model-file -m           : [Required] Model file to register.
    --schema-file -s          : Schema file to add to the manifest.
    -f                        : [Required] The code file to be deployed.
    -p                        : A pip requirements.txt file needed by the code file.
    -r                        : [Required] Runtime of the web service. Valid runtimes are python|spark-py.


## <a name="service-commands"></a><span data-ttu-id="a4ef8-143">Service commands</span><span class="sxs-lookup"><span data-stu-id="a4ef8-143">Service commands</span></span>
<span data-ttu-id="a4ef8-144">The following commands are supported for Service.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-144">The following commands are supported for Service.</span></span> <span data-ttu-id="a4ef8-145">To see the parameters for each command, use the -h option.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-145">To see the parameters for each command, use the -h option.</span></span> <span data-ttu-id="a4ef8-146">For example, use `az ml service create realtime -h` to see create command details.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-146">For example, use `az ml service create realtime -h` to see create command details.</span></span>

    create
    delete
    keys
    list
    logs
    run
    show
    update
    usage

<span data-ttu-id="a4ef8-147">**Create a service**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-147">**Create a service**</span></span>

<span data-ttu-id="a4ef8-148">To create a service with a previously created image, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-148">To create a service with a previously created image, use the following command:</span></span>

`az ml service create realtime --image-id [image to deploy] -n [service name]`

<span data-ttu-id="a4ef8-149">To create a service, manifest, and image with a single command, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-149">To create a service, manifest, and image with a single command, use the following command:</span></span>

`az ml service create realtime --model-file [path to model file(s)] -f [path to model scoring file, e.g. score.py] -n [service name] -r [run time included in the image, e.g. spark-py]`

<span data-ttu-id="a4ef8-150">Commands details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-150">Commands details:</span></span>

    -n                                : [Required] Webservice name.
    --autoscale-enabled               : Enable automatic scaling of service replicas based on request demand.
                                        Allowed values: true, false. False if omitted.  Default: false.
    --autoscale-max-replicas          : If autoscale is enabled - sets the maximum number of replicas.
    --autoscale-min-replicas          : If autoscale is enabled - sets the minimum number of replicas.
    --autoscale-refresh-period-seconds: If autoscale is enabled - the interval of evaluating scaling demand.
    --autoscale-target-utilization    : If autoscale is enabled - target utilization of replicas time.
    --collect-model-data              : Enable model data collection. Allowed values: true, false. False if omitted.  Default: false.
    --cpu                             : Reserved number of CPU cores per service replica (can be fraction).
    --enable-app-insights -l          : Enable app insights. Allowed values: true, false. False if omitted.  Default: false.
    --memory                          : Reserved amount of memory per service replica, in M or G. (ex. 1G, 300M).
    --replica-max-concurrent-requests : Maximum number of concurrent requests that can be routed to a service replica.
    -v                                : Verbosity flag.
    -z                                : Number of replicas for a Kubernetes service.  Default: 1.

<span data-ttu-id="a4ef8-151">Registered Image Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-151">Registered Image Arguments</span></span>

    --image-id                        : [Required] Image to deploy to the service.

<span data-ttu-id="a4ef8-152">Unregistered Image Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-152">Unregistered Image Arguments</span></span>

    --conda-file -c                   : Path to Conda Environment file.
    --image-type                      : The image type to create. Defaults to "Docker".
    --model-file -m                   : [Required] The model to be deployed.
    -d                                : Files and directories required by the service. Multiple dependencies can be specified
                                        with additional -d arguments.
    -f                                : [Required] The code file to be deployed.
    -p                                : A pip requirements.txt file of package needed by the code file.
    -r                                : [Required] Runtime of the web service. Valid runtimes are python|spark-py.
    -s                                : Input and output schema of the web service.

<span data-ttu-id="a4ef8-153">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-153">Global Arguments</span></span>

    --debug                           : Increase logging verbosity to show all debug logs.
    --help -h                         : Show this help message and exit.
    --output -o                       : Output format.  Allowed values: json, jsonc, table, tsv. Default: json.
    --query                           : JMESPath query string. See http://jmespath.org/ for more information and examples.
    --verbose                         : Increase logging verbosity. Use --debug for full debug logs.


<span data-ttu-id="a4ef8-154">Note on the `-d` flag for attaching dependencies: If you pass the name of a directory that is not already bundled (zip, tar, etc.), that directory automatically gets tar’ed and is passed along, then automatically unbundled on the other end.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-154">Note on the `-d` flag for attaching dependencies: If you pass the name of a directory that is not already bundled (zip, tar, etc.), that directory automatically gets tar’ed and is passed along, then automatically unbundled on the other end.</span></span> 

<span data-ttu-id="a4ef8-155">If you pass in a directory that is already bundled, the directory is treated as a file and passed along as is.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-155">If you pass in a directory that is already bundled, the directory is treated as a file and passed along as is.</span></span> <span data-ttu-id="a4ef8-156">It is unbundled automatically; you are expected to handle that in your code.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-156">It is unbundled automatically; you are expected to handle that in your code.</span></span>

<span data-ttu-id="a4ef8-157">**Get service details**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-157">**Get service details**</span></span>

<span data-ttu-id="a4ef8-158">Get service details including URL, usage (including sample data if a schema was created).</span><span class="sxs-lookup"><span data-stu-id="a4ef8-158">Get service details including URL, usage (including sample data if a schema was created).</span></span>

`az ml service show realtime --name [service name]`

<span data-ttu-id="a4ef8-159">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-159">Command details:</span></span>

    --id -i    : The service id to show.
    --name -n  : Webservice name.
    -v         : Verbosity flag.

<span data-ttu-id="a4ef8-160">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-160">Global Arguments</span></span>

    --debug    : Increase logging verbosity to show all debug logs.
    --help -h  : Show this help message and exit.
    --output -o: Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
    --query    : JMESPath query string. See http://jmespath.org/ for more information and examples.
    --verbose  : Increase logging verbosity. Use --debug for full debug logs.

<span data-ttu-id="a4ef8-161">**Run the service**</span><span class="sxs-lookup"><span data-stu-id="a4ef8-161">**Run the service**</span></span>

`az ml service run realtime -n [service name] -d [input_data]`

<span data-ttu-id="a4ef8-162">Command details:</span><span class="sxs-lookup"><span data-stu-id="a4ef8-162">Command details:</span></span>

    --id -i    : The service id to show.
    --name -n  : Webservice name.
    -v         : Verbosity flag.

<span data-ttu-id="a4ef8-163">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-163">Global Arguments</span></span>

    --debug    : Increase logging verbosity to show all debug logs.
    --help -h  : Show this help message and exit.
    --output -o: Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
    --query    : JMESPath query string. See http://jmespath.org/ for more information and examples.
    --verbose  : Increase logging verbosity. Use --debug for full debug logs.

<span data-ttu-id="a4ef8-164">Command</span><span class="sxs-lookup"><span data-stu-id="a4ef8-164">Command</span></span>

    az ml service run realtime

<span data-ttu-id="a4ef8-165">Arguments --id -i    : [Required] The service id to score against.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-165">Arguments --id -i    : [Required] The service id to score against.</span></span>
<span data-ttu-id="a4ef8-166">-d         : The data to use for calling the web service.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-166">-d         : The data to use for calling the web service.</span></span>
<span data-ttu-id="a4ef8-167">-v         : Verbosity flag.</span><span class="sxs-lookup"><span data-stu-id="a4ef8-167">-v         : Verbosity flag.</span></span>

<span data-ttu-id="a4ef8-168">Global Arguments</span><span class="sxs-lookup"><span data-stu-id="a4ef8-168">Global Arguments</span></span>

    --debug    : Increase logging verbosity to show all debug logs.
    --help -h  : Show this help message and exit.
    --output -o: Output format.  Allowed values: json, jsonc, table, tsv. Default: json.
    --query    : JMESPath query string. See http://jmespath.org/ for more information and examples.
    --verbose  : Increase logging verbosity. Use --debug for full debug logs.
