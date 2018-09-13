---
title: Azure Machine Learning Model Management Web Service Deployment | Microsoft Docs
description: This document describes the steps involved in deploying a machine learning model using Azure Machine Learning model Management.
services: machine-learning
author: aashishb
ms.author: aashishb
manager: hjerez
ms.reviewer: jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 01/03/2018
ms.openlocfilehash: f6bb6f3fbafe9b529d483af8edd55e16a35e703a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856973"
---
# <a name="deploying-a-machine-learning-model-as-a-web-service"></a><span data-ttu-id="52ca3-103">Deploying a Machine Learning Model as a web service</span><span class="sxs-lookup"><span data-stu-id="52ca3-103">Deploying a Machine Learning Model as a web service</span></span>

<span data-ttu-id="52ca3-104">Azure Machine Learning Model Management provides interfaces to deploy models as containerized Docker-based web services.</span><span class="sxs-lookup"><span data-stu-id="52ca3-104">Azure Machine Learning Model Management provides interfaces to deploy models as containerized Docker-based web services.</span></span> <span data-ttu-id="52ca3-105">You can deploy models you create using frameworks such as Spark, the Microsoft Cognitive Toolkit (CNTK), Keras, Tensorflow, and Python.</span><span class="sxs-lookup"><span data-stu-id="52ca3-105">You can deploy models you create using frameworks such as Spark, the Microsoft Cognitive Toolkit (CNTK), Keras, Tensorflow, and Python.</span></span> 

<span data-ttu-id="52ca3-106">This document covers the steps to deploy your models as web services using the Azure Machine Learning Model Management command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="52ca3-106">This document covers the steps to deploy your models as web services using the Azure Machine Learning Model Management command-line interface (CLI).</span></span>

## <a name="what-you-need-to-get-started"></a><span data-ttu-id="52ca3-107">What you need to get started</span><span class="sxs-lookup"><span data-stu-id="52ca3-107">What you need to get started</span></span>

<span data-ttu-id="52ca3-108">To get the most out of this guide, you should have contributer access to an Azure subscription or a resource group that you can deploy your models to.</span><span class="sxs-lookup"><span data-stu-id="52ca3-108">To get the most out of this guide, you should have contributer access to an Azure subscription or a resource group that you can deploy your models to.</span></span>
<span data-ttu-id="52ca3-109">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span><span class="sxs-lookup"><span data-stu-id="52ca3-109">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span></span>  <span data-ttu-id="52ca3-110">It can also be installed as a stand-alone package.</span><span class="sxs-lookup"><span data-stu-id="52ca3-110">It can also be installed as a stand-alone package.</span></span>

<span data-ttu-id="52ca3-111">In addition, a model management account and deployment environment must already be set up.</span><span class="sxs-lookup"><span data-stu-id="52ca3-111">In addition, a model management account and deployment environment must already be set up.</span></span>  <span data-ttu-id="52ca3-112">For more info on setting up your model management account and environment for local and cluster deployment, see [Model Management configuration](deployment-setup-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="52ca3-112">For more info on setting up your model management account and environment for local and cluster deployment, see [Model Management configuration](deployment-setup-configuration.md).</span></span>

## <a name="deploying-web-services"></a><span data-ttu-id="52ca3-113">Deploying web services</span><span class="sxs-lookup"><span data-stu-id="52ca3-113">Deploying web services</span></span>
<span data-ttu-id="52ca3-114">Using the CLIs, you can deploy web services to run on the local machine or on a cluster.</span><span class="sxs-lookup"><span data-stu-id="52ca3-114">Using the CLIs, you can deploy web services to run on the local machine or on a cluster.</span></span>

<span data-ttu-id="52ca3-115">We recommend starting with a local deployment.</span><span class="sxs-lookup"><span data-stu-id="52ca3-115">We recommend starting with a local deployment.</span></span> <span data-ttu-id="52ca3-116">You first validate that your model and code work, then deploy the web service to a cluster for production-scale use.</span><span class="sxs-lookup"><span data-stu-id="52ca3-116">You first validate that your model and code work, then deploy the web service to a cluster for production-scale use.</span></span>

<span data-ttu-id="52ca3-117">The following are the deployment steps:</span><span class="sxs-lookup"><span data-stu-id="52ca3-117">The following are the deployment steps:</span></span>
1. <span data-ttu-id="52ca3-118">Use your saved, trained, Machine Learning model</span><span class="sxs-lookup"><span data-stu-id="52ca3-118">Use your saved, trained, Machine Learning model</span></span>
2. <span data-ttu-id="52ca3-119">Create a schema for your web service's input and output data</span><span class="sxs-lookup"><span data-stu-id="52ca3-119">Create a schema for your web service's input and output data</span></span>
3. <span data-ttu-id="52ca3-120">Create a Docker-based container image</span><span class="sxs-lookup"><span data-stu-id="52ca3-120">Create a Docker-based container image</span></span>
4. <span data-ttu-id="52ca3-121">Create and deploy the web service</span><span class="sxs-lookup"><span data-stu-id="52ca3-121">Create and deploy the web service</span></span>

### <a name="1-save-your-model"></a><span data-ttu-id="52ca3-122">1. Save your model</span><span class="sxs-lookup"><span data-stu-id="52ca3-122">1. Save your model</span></span>
<span data-ttu-id="52ca3-123">Start with your saved trained model file, for example, mymodel.pkl.</span><span class="sxs-lookup"><span data-stu-id="52ca3-123">Start with your saved trained model file, for example, mymodel.pkl.</span></span> <span data-ttu-id="52ca3-124">The file extension varies based on the platform you use to train and save the model.</span><span class="sxs-lookup"><span data-stu-id="52ca3-124">The file extension varies based on the platform you use to train and save the model.</span></span> 

<span data-ttu-id="52ca3-125">As an example, you can use Python's Pickle library to save a trained model to a file.</span><span class="sxs-lookup"><span data-stu-id="52ca3-125">As an example, you can use Python's Pickle library to save a trained model to a file.</span></span> <span data-ttu-id="52ca3-126">Here is an [example](http://scikit-learn.org/stable/modules/model_persistence.html) using the Iris dataset:</span><span class="sxs-lookup"><span data-stu-id="52ca3-126">Here is an [example](http://scikit-learn.org/stable/modules/model_persistence.html) using the Iris dataset:</span></span>

```python
import pickle
from sklearn import datasets
iris = datasets.load_iris()
X, y = iris.data, iris.target
clf = linear_model.LogisticRegression()
clf.fit(X, y)  
saved_model = pickle.dumps(clf)
```

### <a name="2-create-a-schemajson-file"></a><span data-ttu-id="52ca3-127">2. Create a schema.json file</span><span class="sxs-lookup"><span data-stu-id="52ca3-127">2. Create a schema.json file</span></span>

<span data-ttu-id="52ca3-128">While schema generation is optional, it is highly recommended to define the request and input variable format for better handling.</span><span class="sxs-lookup"><span data-stu-id="52ca3-128">While schema generation is optional, it is highly recommended to define the request and input variable format for better handling.</span></span>

<span data-ttu-id="52ca3-129">Create a schema to automatically validate the input and output of your web service.</span><span class="sxs-lookup"><span data-stu-id="52ca3-129">Create a schema to automatically validate the input and output of your web service.</span></span> <span data-ttu-id="52ca3-130">The CLIs also use the schema to generate a Swagger document for your web service.</span><span class="sxs-lookup"><span data-stu-id="52ca3-130">The CLIs also use the schema to generate a Swagger document for your web service.</span></span>

<span data-ttu-id="52ca3-131">To create the schema, import the following libraries:</span><span class="sxs-lookup"><span data-stu-id="52ca3-131">To create the schema, import the following libraries:</span></span>

```python
from azureml.api.schema.dataTypes import DataTypes
from azureml.api.schema.sampleDefinition import SampleDefinition
from azureml.api.realtime.services import generate_schema
```
<span data-ttu-id="52ca3-132">Next, define the input variables such as a Spark dataframe, Pandas dataframe, or NumPy array.</span><span class="sxs-lookup"><span data-stu-id="52ca3-132">Next, define the input variables such as a Spark dataframe, Pandas dataframe, or NumPy array.</span></span> <span data-ttu-id="52ca3-133">The following example uses a Numpy array:</span><span class="sxs-lookup"><span data-stu-id="52ca3-133">The following example uses a Numpy array:</span></span>

```python
inputs = {"input_array": SampleDefinition(DataTypes.NUMPY, yourinputarray)}
generate_schema(run_func=run, inputs=inputs, filepath='./outputs/service_schema.json')
```
<span data-ttu-id="52ca3-134">The following example uses a Spark dataframe:</span><span class="sxs-lookup"><span data-stu-id="52ca3-134">The following example uses a Spark dataframe:</span></span>

```python
inputs = {"input_df": SampleDefinition(DataTypes.SPARK, yourinputdataframe)}
generate_schema(run_func=run, inputs=inputs, filepath='./outputs/service_schema.json')
```

<span data-ttu-id="52ca3-135">The following example uses a PANDAS dataframe:</span><span class="sxs-lookup"><span data-stu-id="52ca3-135">The following example uses a PANDAS dataframe:</span></span>

```python
inputs = {"input_df": SampleDefinition(DataTypes.PANDAS, yourinputdataframe)}
generate_schema(run_func=run, inputs=inputs, filepath='./outputs/service_schema.json')
```

<span data-ttu-id="52ca3-136">The following example uses a generic JSON format:</span><span class="sxs-lookup"><span data-stu-id="52ca3-136">The following example uses a generic JSON format:</span></span>

```python
inputs = {"input_json": SampleDefinition(DataTypes.STANDARD, yourinputjson)}
generate_schema(run_func=run, inputs=inputs, filepath='./outputs/service_schema.json')
```

### <a name="3-create-a-scorepy-file"></a><span data-ttu-id="52ca3-137">3. Create a score.py file</span><span class="sxs-lookup"><span data-stu-id="52ca3-137">3. Create a score.py file</span></span>
<span data-ttu-id="52ca3-138">You provide a score.py file, which loads your model and returns the prediction result(s) using the model.</span><span class="sxs-lookup"><span data-stu-id="52ca3-138">You provide a score.py file, which loads your model and returns the prediction result(s) using the model.</span></span>

<span data-ttu-id="52ca3-139">The file must include two functions: init and run.</span><span class="sxs-lookup"><span data-stu-id="52ca3-139">The file must include two functions: init and run.</span></span>

<span data-ttu-id="52ca3-140">Add following code at the top of the score.py file to enable data collection functionality that helps collect model input and prediction data</span><span class="sxs-lookup"><span data-stu-id="52ca3-140">Add following code at the top of the score.py file to enable data collection functionality that helps collect model input and prediction data</span></span>

```python
from azureml.datacollector import ModelDataCollector
```

<span data-ttu-id="52ca3-141">Check [model data collection](how-to-use-model-data-collection.md) section for more details on how to use this feature.</span><span class="sxs-lookup"><span data-stu-id="52ca3-141">Check [model data collection](how-to-use-model-data-collection.md) section for more details on how to use this feature.</span></span>

#### <a name="init-function"></a><span data-ttu-id="52ca3-142">Init function</span><span class="sxs-lookup"><span data-stu-id="52ca3-142">Init function</span></span>
<span data-ttu-id="52ca3-143">Use the init function to load the saved model.</span><span class="sxs-lookup"><span data-stu-id="52ca3-143">Use the init function to load the saved model.</span></span>

<span data-ttu-id="52ca3-144">Example of a simple init function loading the model:</span><span class="sxs-lookup"><span data-stu-id="52ca3-144">Example of a simple init function loading the model:</span></span>

```python
def init():  
    from sklearn.externals import joblib
    global model, inputs_dc, prediction_dc
    model = joblib.load('model.pkl')

    inputs_dc = ModelDataCollector('model.pkl',identifier="inputs")
    prediction_dc = ModelDataCollector('model.pkl', identifier="prediction")
```

#### <a name="run-function"></a><span data-ttu-id="52ca3-145">Run function</span><span class="sxs-lookup"><span data-stu-id="52ca3-145">Run function</span></span>
<span data-ttu-id="52ca3-146">The run function uses the model and the input data to return a prediction.</span><span class="sxs-lookup"><span data-stu-id="52ca3-146">The run function uses the model and the input data to return a prediction.</span></span>

<span data-ttu-id="52ca3-147">Example of a simple run function processing the input and returning the prediction result:</span><span class="sxs-lookup"><span data-stu-id="52ca3-147">Example of a simple run function processing the input and returning the prediction result:</span></span>

```python
def run(input_df):
    global clf2, inputs_dc, prediction_dc
    try:
        prediction = model.predict(input_df)
        inputs_dc.collect(input_df)
        prediction_dc.collect(prediction)
        return prediction
    except Exception as e:
        return (str(e))
```

### <a name="4-register-a-model"></a><span data-ttu-id="52ca3-148">4. Register a model</span><span class="sxs-lookup"><span data-stu-id="52ca3-148">4. Register a model</span></span>
<span data-ttu-id="52ca3-149">Following command is used to register a model created in step 1 above,</span><span class="sxs-lookup"><span data-stu-id="52ca3-149">Following command is used to register a model created in step 1 above,</span></span>

```
az ml model register --model [path to model file] --name [model name]
```

### <a name="5-create-manifest"></a><span data-ttu-id="52ca3-150">5. Create manifest</span><span class="sxs-lookup"><span data-stu-id="52ca3-150">5. Create manifest</span></span>
<span data-ttu-id="52ca3-151">Following command helps create a manifest for the model,</span><span class="sxs-lookup"><span data-stu-id="52ca3-151">Following command helps create a manifest for the model,</span></span>

```
az ml manifest create --manifest-name [your new manifest name] -f [path to score file] -r [runtime for the image, e.g. spark-py]
```
<span data-ttu-id="52ca3-152">You can add a previously registered model to the manifest by using argument `--model-id` or `-i` in the command shown above.</span><span class="sxs-lookup"><span data-stu-id="52ca3-152">You can add a previously registered model to the manifest by using argument `--model-id` or `-i` in the command shown above.</span></span> <span data-ttu-id="52ca3-153">Multiple models can be specified with additional -i arguments.</span><span class="sxs-lookup"><span data-stu-id="52ca3-153">Multiple models can be specified with additional -i arguments.</span></span>

### <a name="6-create-an-image"></a><span data-ttu-id="52ca3-154">6. Create an image</span><span class="sxs-lookup"><span data-stu-id="52ca3-154">6. Create an image</span></span> 
<span data-ttu-id="52ca3-155">You can create an image with the option of having created its manifest before.</span><span class="sxs-lookup"><span data-stu-id="52ca3-155">You can create an image with the option of having created its manifest before.</span></span> 

```
az ml image create -n [image name] --manifest-id [the manifest ID]
```

>[!NOTE] 
><span data-ttu-id="52ca3-156">You can also use a single command to perform the model registration, manifest and model creation.</span><span class="sxs-lookup"><span data-stu-id="52ca3-156">You can also use a single command to perform the model registration, manifest and model creation.</span></span> <span data-ttu-id="52ca3-157">Use -h with the service create command for more details.</span><span class="sxs-lookup"><span data-stu-id="52ca3-157">Use -h with the service create command for more details.</span></span>

<span data-ttu-id="52ca3-158">As an alternative, there is a single command to register a model, create a manifest and create an image (but not create and deploy the web service, yet) as one step as follows.</span><span class="sxs-lookup"><span data-stu-id="52ca3-158">As an alternative, there is a single command to register a model, create a manifest and create an image (but not create and deploy the web service, yet) as one step as follows.</span></span>

```
az ml image create -n [image name] --model-file [model file or folder path] -f [code file, e.g. the score.py file] -r [the runtime e.g. spark-py which is the Docker container image base]
```

>[!NOTE]
><span data-ttu-id="52ca3-159">For more details on the command parameters, type -h at the end of the command for example, az ml image create -h.</span><span class="sxs-lookup"><span data-stu-id="52ca3-159">For more details on the command parameters, type -h at the end of the command for example, az ml image create -h.</span></span>


### <a name="7-create-and-deploy-the-web-service"></a><span data-ttu-id="52ca3-160">7. Create and deploy the web service</span><span class="sxs-lookup"><span data-stu-id="52ca3-160">7. Create and deploy the web service</span></span>
<span data-ttu-id="52ca3-161">Deploy the service using the following command:</span><span class="sxs-lookup"><span data-stu-id="52ca3-161">Deploy the service using the following command:</span></span>

```
az ml service create realtime --image-id <image id> -n <service name>
```

>[!NOTE] 
><span data-ttu-id="52ca3-162">You can also use a single command to perform all previous 4 steps.</span><span class="sxs-lookup"><span data-stu-id="52ca3-162">You can also use a single command to perform all previous 4 steps.</span></span> <span data-ttu-id="52ca3-163">Use -h with the service create command for more details.</span><span class="sxs-lookup"><span data-stu-id="52ca3-163">Use -h with the service create command for more details.</span></span>

<span data-ttu-id="52ca3-164">As an alternative, there is a single command to register a model, create a manifest, create an image, as well as, create and deploy the webservice, as one step as follows.</span><span class="sxs-lookup"><span data-stu-id="52ca3-164">As an alternative, there is a single command to register a model, create a manifest, create an image, as well as, create and deploy the webservice, as one step as follows.</span></span>

```azurecli
az ml service create realtime --model-file [model file/folder path] -f [scoring file e.g. score.py] -n [your service name] -s [schema file e.g. service_schema.json] -r [runtime for the Docker container e.g. spark-py or python] -c [conda dependencies file for additional python packages]
```


### <a name="8-test-the-service"></a><span data-ttu-id="52ca3-165">8. Test the service</span><span class="sxs-lookup"><span data-stu-id="52ca3-165">8. Test the service</span></span>
<span data-ttu-id="52ca3-166">Use the following command to get information on how to call the service:</span><span class="sxs-lookup"><span data-stu-id="52ca3-166">Use the following command to get information on how to call the service:</span></span>

```
az ml service usage realtime -i <service id>
```

<span data-ttu-id="52ca3-167">Call the service using the run function from the command prompt:</span><span class="sxs-lookup"><span data-stu-id="52ca3-167">Call the service using the run function from the command prompt:</span></span>

```
az ml service run realtime -i <service id> -d "{\"input_df\": [INPUT DATA]}"
```

<span data-ttu-id="52ca3-168">The following example calls a sample Iris web service:</span><span class="sxs-lookup"><span data-stu-id="52ca3-168">The following example calls a sample Iris web service:</span></span>

```
az ml service run realtime -i <service id> -d "{\"input_df\": [{\"sepal length\": 3.0, \"sepal width\": 3.6, \"petal width\": 1.3, \"petal length\":0.25}]}"
```

## <a name="next-steps"></a><span data-ttu-id="52ca3-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="52ca3-169">Next steps</span></span>
<span data-ttu-id="52ca3-170">Now that you have tested your web service to run locally, you can deploy it to a cluster for large-scale use.</span><span class="sxs-lookup"><span data-stu-id="52ca3-170">Now that you have tested your web service to run locally, you can deploy it to a cluster for large-scale use.</span></span> <span data-ttu-id="52ca3-171">For details on setting up a cluster for web service deployment, see [Model Management Configuration](deployment-setup-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="52ca3-171">For details on setting up a cluster for web service deployment, see [Model Management Configuration](deployment-setup-configuration.md).</span></span> 
