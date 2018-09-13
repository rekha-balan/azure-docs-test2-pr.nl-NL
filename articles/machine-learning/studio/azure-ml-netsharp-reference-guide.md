---
title: Net# Neural Networks Specification Language Guide - Azure Machine Learning | Microsoft Docs
description: Syntax for the Net# neural networks specification language, together with examples of how to create a custom neural network model using Net#
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 03/01/2018
ms.openlocfilehash: 887d3d719f92447f247d4372f873b892dd55207e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967129"
---
# <a name="guide-to-net-neural-network-specification-language-for-azure-machine-learning"></a><span data-ttu-id="efc63-103">Guide to Net# neural network specification language for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="efc63-103">Guide to Net# neural network specification language for Azure Machine Learning</span></span>

<span data-ttu-id="efc63-104">Net# is a language developed by Microsoft that is used to define neural network architectures.</span><span class="sxs-lookup"><span data-stu-id="efc63-104">Net# is a language developed by Microsoft that is used to define neural network architectures.</span></span> <span data-ttu-id="efc63-105">Using Net# to define the structure of a neural network makes it possible to define complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known to improve learning on data such as image, audio, or video.</span><span class="sxs-lookup"><span data-stu-id="efc63-105">Using Net# to define the structure of a neural network makes it possible to define complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known to improve learning on data such as image, audio, or video.</span></span>

<span data-ttu-id="efc63-106">You can use a Net# architecture specification in these contexts:</span><span class="sxs-lookup"><span data-stu-id="efc63-106">You can use a Net# architecture specification in these contexts:</span></span>

+ <span data-ttu-id="efc63-107">All neural network modules in Microsoft Azure Machine Learning Studio: [Multiclass Neural Network](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/multiclass-neural-network), [Two-Class Neural Network](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/two-class-neural-network), and [Neural Network Regression](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/neural-network-regression)</span><span class="sxs-lookup"><span data-stu-id="efc63-107">All neural network modules in Microsoft Azure Machine Learning Studio: [Multiclass Neural Network](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/multiclass-neural-network), [Two-Class Neural Network](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/two-class-neural-network), and [Neural Network Regression](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/neural-network-regression)</span></span>
+ <span data-ttu-id="efc63-108">Neural network functions in MicrosoftML: [NeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/neuralnet) and [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)for the R language, and [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) for Python.</span><span class="sxs-lookup"><span data-stu-id="efc63-108">Neural network functions in MicrosoftML: [NeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/neuralnet) and [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)for the R language, and [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) for Python.</span></span>


<span data-ttu-id="efc63-109">This article describes the basic concepts and syntax needed to develop a custom neural network using Net#:</span><span class="sxs-lookup"><span data-stu-id="efc63-109">This article describes the basic concepts and syntax needed to develop a custom neural network using Net#:</span></span> 

+ <span data-ttu-id="efc63-110">Neural network requirements and how to define the primary components</span><span class="sxs-lookup"><span data-stu-id="efc63-110">Neural network requirements and how to define the primary components</span></span>
+ <span data-ttu-id="efc63-111">The syntax and keywords of the Net# specification language</span><span class="sxs-lookup"><span data-stu-id="efc63-111">The syntax and keywords of the Net# specification language</span></span>
+ <span data-ttu-id="efc63-112">Examples of custom neural networks created using Net#</span><span class="sxs-lookup"><span data-stu-id="efc63-112">Examples of custom neural networks created using Net#</span></span> 

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a><span data-ttu-id="efc63-113">Neural network basics</span><span class="sxs-lookup"><span data-stu-id="efc63-113">Neural network basics</span></span>

<span data-ttu-id="efc63-114">A neural network structure consists of nodes that are organized in layers, and weighted connections (or edges) between the nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-114">A neural network structure consists of nodes that are organized in layers, and weighted connections (or edges) between the nodes.</span></span> <span data-ttu-id="efc63-115">The connections are directional, and each connection has a source node and a destination node.</span><span class="sxs-lookup"><span data-stu-id="efc63-115">The connections are directional, and each connection has a source node and a destination node.</span></span>  

<span data-ttu-id="efc63-116">Each trainable layer (a hidden or an output layer) has one or more **connection bundles**.</span><span class="sxs-lookup"><span data-stu-id="efc63-116">Each trainable layer (a hidden or an output layer) has one or more **connection bundles**.</span></span> <span data-ttu-id="efc63-117">A connection bundle consists of a source layer and a specification of the connections from that source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-117">A connection bundle consists of a source layer and a specification of the connections from that source layer.</span></span> <span data-ttu-id="efc63-118">All the connections in a given bundle share the same source layer and the same destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-118">All the connections in a given bundle share the same source layer and the same destination layer.</span></span> <span data-ttu-id="efc63-119">In Net#, a connection bundle is considered as belonging to the bundle's destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-119">In Net#, a connection bundle is considered as belonging to the bundle's destination layer.</span></span>

<span data-ttu-id="efc63-120">Net# supports various kinds of connection bundles, which lets you customize the way inputs are mapped to hidden layers and mapped to the outputs.</span><span class="sxs-lookup"><span data-stu-id="efc63-120">Net# supports various kinds of connection bundles, which lets you customize the way inputs are mapped to hidden layers and mapped to the outputs.</span></span>

<span data-ttu-id="efc63-121">The default or standard bundle is a **full bundle**, in which each node in the source layer is connected to every node in the destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-121">The default or standard bundle is a **full bundle**, in which each node in the source layer is connected to every node in the destination layer.</span></span>

<span data-ttu-id="efc63-122">Additionally, Net# supports the following four kinds of advanced connection bundles:</span><span class="sxs-lookup"><span data-stu-id="efc63-122">Additionally, Net# supports the following four kinds of advanced connection bundles:</span></span>

+ <span data-ttu-id="efc63-123">**Filtered bundles**.</span><span class="sxs-lookup"><span data-stu-id="efc63-123">**Filtered bundles**.</span></span> <span data-ttu-id="efc63-124">The user can define a predicate by using the locations of the source layer node and the destination layer node.</span><span class="sxs-lookup"><span data-stu-id="efc63-124">The user can define a predicate by using the locations of the source layer node and the destination layer node.</span></span> <span data-ttu-id="efc63-125">Nodes are connected whenever the predicate is True.</span><span class="sxs-lookup"><span data-stu-id="efc63-125">Nodes are connected whenever the predicate is True.</span></span>

+ <span data-ttu-id="efc63-126">**Convolutional bundles**.</span><span class="sxs-lookup"><span data-stu-id="efc63-126">**Convolutional bundles**.</span></span> <span data-ttu-id="efc63-127">The user can define small neighborhoods of nodes in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-127">The user can define small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="efc63-128">Each node in the destination layer is connected to one neighborhood of nodes in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-128">Each node in the destination layer is connected to one neighborhood of nodes in the source layer.</span></span>

+ <span data-ttu-id="efc63-129">**Pooling bundles** and **Response normalization bundles**.</span><span class="sxs-lookup"><span data-stu-id="efc63-129">**Pooling bundles** and **Response normalization bundles**.</span></span> <span data-ttu-id="efc63-130">These are similar to convolutional bundles in that the user defines small neighborhoods of nodes in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-130">These are similar to convolutional bundles in that the user defines small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="efc63-131">The difference is that the weights of the edges in these bundles are not trainable.</span><span class="sxs-lookup"><span data-stu-id="efc63-131">The difference is that the weights of the edges in these bundles are not trainable.</span></span> <span data-ttu-id="efc63-132">Instead, a predefined function is applied to the source node values to determine the destination node value.</span><span class="sxs-lookup"><span data-stu-id="efc63-132">Instead, a predefined function is applied to the source node values to determine the destination node value.</span></span>


## <a name="supported-customizations"></a><span data-ttu-id="efc63-133">Supported customizations</span><span class="sxs-lookup"><span data-stu-id="efc63-133">Supported customizations</span></span>

<span data-ttu-id="efc63-134">The architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span><span class="sxs-lookup"><span data-stu-id="efc63-134">The architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span></span> <span data-ttu-id="efc63-135">You can:</span><span class="sxs-lookup"><span data-stu-id="efc63-135">You can:</span></span>

+ <span data-ttu-id="efc63-136">Create hidden layers and control the number of nodes in each layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-136">Create hidden layers and control the number of nodes in each layer.</span></span>
+ <span data-ttu-id="efc63-137">Specify how layers are to be connected to each other.</span><span class="sxs-lookup"><span data-stu-id="efc63-137">Specify how layers are to be connected to each other.</span></span>
+ <span data-ttu-id="efc63-138">Define special connectivity structures, such as convolutions and weight sharing bundles.</span><span class="sxs-lookup"><span data-stu-id="efc63-138">Define special connectivity structures, such as convolutions and weight sharing bundles.</span></span>
+ <span data-ttu-id="efc63-139">Specify different activation functions.</span><span class="sxs-lookup"><span data-stu-id="efc63-139">Specify different activation functions.</span></span>

<span data-ttu-id="efc63-140">For details of the specification language syntax, see [Structure Specification](#Structure-specifications).</span><span class="sxs-lookup"><span data-stu-id="efc63-140">For details of the specification language syntax, see [Structure Specification](#Structure-specifications).</span></span>  

<span data-ttu-id="efc63-141">For examples of defining neural networks for some common machine learning tasks, from simplex to complex, see [Examples](#Examples-of-Net#-usage).</span><span class="sxs-lookup"><span data-stu-id="efc63-141">For examples of defining neural networks for some common machine learning tasks, from simplex to complex, see [Examples](#Examples-of-Net#-usage).</span></span>

## <a name="general-requirements"></a><span data-ttu-id="efc63-142">General requirements</span><span class="sxs-lookup"><span data-stu-id="efc63-142">General requirements</span></span>

+ <span data-ttu-id="efc63-143">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-143">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span></span> 
+ <span data-ttu-id="efc63-144">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span><span class="sxs-lookup"><span data-stu-id="efc63-144">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span></span> 
+ <span data-ttu-id="efc63-145">Input layers have no associated trained parameters and represent the point where instance data enters the network.</span><span class="sxs-lookup"><span data-stu-id="efc63-145">Input layers have no associated trained parameters and represent the point where instance data enters the network.</span></span> 
+ <span data-ttu-id="efc63-146">Trainable layers (the hidden and output layers) have associated trained parameters, known as weights and biases.</span><span class="sxs-lookup"><span data-stu-id="efc63-146">Trainable layers (the hidden and output layers) have associated trained parameters, known as weights and biases.</span></span> 
+ <span data-ttu-id="efc63-147">The source and destination nodes must be in separate layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-147">The source and destination nodes must be in separate layers.</span></span> 
+ <span data-ttu-id="efc63-148">Connections must be acyclic; in other words, there cannot be a chain of connections leading back to the initial source node.</span><span class="sxs-lookup"><span data-stu-id="efc63-148">Connections must be acyclic; in other words, there cannot be a chain of connections leading back to the initial source node.</span></span>
+ <span data-ttu-id="efc63-149">The output layer cannot be a source layer of a connection bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-149">The output layer cannot be a source layer of a connection bundle.</span></span>  

## <a name="structure-specifications"></a><span data-ttu-id="efc63-150">Structure specifications</span><span class="sxs-lookup"><span data-stu-id="efc63-150">Structure specifications</span></span>

<span data-ttu-id="efc63-151">A neural network structure specification is composed of three sections: the **constant declaration**, the **layer declaration**, the **connection declaration**.</span><span class="sxs-lookup"><span data-stu-id="efc63-151">A neural network structure specification is composed of three sections: the **constant declaration**, the **layer declaration**, the **connection declaration**.</span></span> <span data-ttu-id="efc63-152">There is also an optional **share declaration** section.</span><span class="sxs-lookup"><span data-stu-id="efc63-152">There is also an optional **share declaration** section.</span></span> <span data-ttu-id="efc63-153">The sections can be specified in any order.</span><span class="sxs-lookup"><span data-stu-id="efc63-153">The sections can be specified in any order.</span></span>

## <a name="constant-declaration"></a><span data-ttu-id="efc63-154">Constant declaration</span><span class="sxs-lookup"><span data-stu-id="efc63-154">Constant declaration</span></span>

<span data-ttu-id="efc63-155">A constant declaration is optional.</span><span class="sxs-lookup"><span data-stu-id="efc63-155">A constant declaration is optional.</span></span> <span data-ttu-id="efc63-156">It provides a means to define values used elsewhere in the neural network definition.</span><span class="sxs-lookup"><span data-stu-id="efc63-156">It provides a means to define values used elsewhere in the neural network definition.</span></span> <span data-ttu-id="efc63-157">The declaration statement consists of an identifier followed by an equal sign and a value expression.</span><span class="sxs-lookup"><span data-stu-id="efc63-157">The declaration statement consists of an identifier followed by an equal sign and a value expression.</span></span>

<span data-ttu-id="efc63-158">For example, the following statement defines a constant `x`:</span><span class="sxs-lookup"><span data-stu-id="efc63-158">For example, the following statement defines a constant `x`:</span></span>  

`Const X = 28;`

<span data-ttu-id="efc63-159">To define two or more constants simultaneously, enclose the identifier names and values in braces, and separate them by using semicolons.</span><span class="sxs-lookup"><span data-stu-id="efc63-159">To define two or more constants simultaneously, enclose the identifier names and values in braces, and separate them by using semicolons.</span></span> <span data-ttu-id="efc63-160">For example:</span><span class="sxs-lookup"><span data-stu-id="efc63-160">For example:</span></span>

`Const { X = 28; Y = 4; }`

<span data-ttu-id="efc63-161">The right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span><span class="sxs-lookup"><span data-stu-id="efc63-161">The right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span></span> <span data-ttu-id="efc63-162">For example:</span><span class="sxs-lookup"><span data-stu-id="efc63-162">For example:</span></span>

`Const { X = 17 * 2; Y = true; }`

## <a name="layer-declaration"></a><span data-ttu-id="efc63-163">Layer declaration</span><span class="sxs-lookup"><span data-stu-id="efc63-163">Layer declaration</span></span>

<span data-ttu-id="efc63-164">The layer declaration is required.</span><span class="sxs-lookup"><span data-stu-id="efc63-164">The layer declaration is required.</span></span> <span data-ttu-id="efc63-165">It defines the size and source of the layer, including its connection bundles and attributes.</span><span class="sxs-lookup"><span data-stu-id="efc63-165">It defines the size and source of the layer, including its connection bundles and attributes.</span></span> <span data-ttu-id="efc63-166">The declaration statement starts with the name of the layer (input, hidden, or output), followed by the dimensions of the layer (a tuple of positive integers).</span><span class="sxs-lookup"><span data-stu-id="efc63-166">The declaration statement starts with the name of the layer (input, hidden, or output), followed by the dimensions of the layer (a tuple of positive integers).</span></span> <span data-ttu-id="efc63-167">For example:</span><span class="sxs-lookup"><span data-stu-id="efc63-167">For example:</span></span>

```Net#
input Data auto;
hidden Hidden[5,20] from Data all;
output Result[2] from Hidden all;  
```

+ <span data-ttu-id="efc63-168">The product of the dimensions is the number of nodes in the layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-168">The product of the dimensions is the number of nodes in the layer.</span></span> <span data-ttu-id="efc63-169">In this example, there are two dimensions [5,20], which means there are  100 nodes in the layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-169">In this example, there are two dimensions [5,20], which means there are  100 nodes in the layer.</span></span>
+ <span data-ttu-id="efc63-170">The layers can be declared in any order, with one exception: If more than one input layer is defined, the order in which they are declared must match the order of features in the input data.</span><span class="sxs-lookup"><span data-stu-id="efc63-170">The layers can be declared in any order, with one exception: If more than one input layer is defined, the order in which they are declared must match the order of features in the input data.</span></span>

<span data-ttu-id="efc63-171">To specify that the number of nodes in a layer be determined automatically, use the `auto` keyword.</span><span class="sxs-lookup"><span data-stu-id="efc63-171">To specify that the number of nodes in a layer be determined automatically, use the `auto` keyword.</span></span> <span data-ttu-id="efc63-172">The `auto` keyword has different effects, depending on the layer:</span><span class="sxs-lookup"><span data-stu-id="efc63-172">The `auto` keyword has different effects, depending on the layer:</span></span>

+ <span data-ttu-id="efc63-173">In an input layer declaration, the number of nodes is the number of features in the input data.</span><span class="sxs-lookup"><span data-stu-id="efc63-173">In an input layer declaration, the number of nodes is the number of features in the input data.</span></span>
+ <span data-ttu-id="efc63-174">In a hidden layer declaration, the number of nodes is the number that is specified by the parameter value for **Number of hidden nodes**.</span><span class="sxs-lookup"><span data-stu-id="efc63-174">In a hidden layer declaration, the number of nodes is the number that is specified by the parameter value for **Number of hidden nodes**.</span></span>
+ <span data-ttu-id="efc63-175">In an output layer declaration, the number of nodes is 2 for two-class classification, 1 for regression, and equal to the number of output nodes for multiclass classification.</span><span class="sxs-lookup"><span data-stu-id="efc63-175">In an output layer declaration, the number of nodes is 2 for two-class classification, 1 for regression, and equal to the number of output nodes for multiclass classification.</span></span>

<span data-ttu-id="efc63-176">For example, the following network definition allows the size of all layers to be automatically determined:</span><span class="sxs-lookup"><span data-stu-id="efc63-176">For example, the following network definition allows the size of all layers to be automatically determined:</span></span>

```Net#
input Data auto;
hidden Hidden auto from Data all;
output Result auto from Hidden all;  
```

<span data-ttu-id="efc63-177">A layer declaration for a trainable layer (the hidden or output layers) can optionally include the output function (also called an activation function), which defaults to **sigmoid** for classification models, and **linear** for regression models.</span><span class="sxs-lookup"><span data-stu-id="efc63-177">A layer declaration for a trainable layer (the hidden or output layers) can optionally include the output function (also called an activation function), which defaults to **sigmoid** for classification models, and **linear** for regression models.</span></span> <span data-ttu-id="efc63-178">Even if you use the default, you can explicitly state the activation function, if desired for clarity.</span><span class="sxs-lookup"><span data-stu-id="efc63-178">Even if you use the default, you can explicitly state the activation function, if desired for clarity.</span></span>

<span data-ttu-id="efc63-179">The following output functions are supported:</span><span class="sxs-lookup"><span data-stu-id="efc63-179">The following output functions are supported:</span></span>

+ <span data-ttu-id="efc63-180">sigmoid</span><span class="sxs-lookup"><span data-stu-id="efc63-180">sigmoid</span></span>
+ <span data-ttu-id="efc63-181">linear</span><span class="sxs-lookup"><span data-stu-id="efc63-181">linear</span></span>
+ <span data-ttu-id="efc63-182">softmax</span><span class="sxs-lookup"><span data-stu-id="efc63-182">softmax</span></span>
+ <span data-ttu-id="efc63-183">rlinear</span><span class="sxs-lookup"><span data-stu-id="efc63-183">rlinear</span></span>
+ <span data-ttu-id="efc63-184">square</span><span class="sxs-lookup"><span data-stu-id="efc63-184">square</span></span>
+ <span data-ttu-id="efc63-185">sqrt</span><span class="sxs-lookup"><span data-stu-id="efc63-185">sqrt</span></span>
+ <span data-ttu-id="efc63-186">srlinear</span><span class="sxs-lookup"><span data-stu-id="efc63-186">srlinear</span></span>
+ <span data-ttu-id="efc63-187">abs</span><span class="sxs-lookup"><span data-stu-id="efc63-187">abs</span></span>
+ <span data-ttu-id="efc63-188">tanh</span><span class="sxs-lookup"><span data-stu-id="efc63-188">tanh</span></span>
+ <span data-ttu-id="efc63-189">brlinear</span><span class="sxs-lookup"><span data-stu-id="efc63-189">brlinear</span></span>

<span data-ttu-id="efc63-190">For example, the following declaration uses the **softmax** function:</span><span class="sxs-lookup"><span data-stu-id="efc63-190">For example, the following declaration uses the **softmax** function:</span></span>

`output Result [100] softmax from Hidden all;`

## <a name="connection-declaration"></a><span data-ttu-id="efc63-191">Connection declaration</span><span class="sxs-lookup"><span data-stu-id="efc63-191">Connection declaration</span></span>

<span data-ttu-id="efc63-192">Immediately after defining the trainable layer, you must declare connections among the layers you have defined.</span><span class="sxs-lookup"><span data-stu-id="efc63-192">Immediately after defining the trainable layer, you must declare connections among the layers you have defined.</span></span> <span data-ttu-id="efc63-193">The connection bundle declaration starts with the keyword `from`, followed by the name of the bundle's source layer and the kind of connection bundle to create.</span><span class="sxs-lookup"><span data-stu-id="efc63-193">The connection bundle declaration starts with the keyword `from`, followed by the name of the bundle's source layer and the kind of connection bundle to create.</span></span>

<span data-ttu-id="efc63-194">Currently, five kinds of connection bundles are supported:</span><span class="sxs-lookup"><span data-stu-id="efc63-194">Currently, five kinds of connection bundles are supported:</span></span>

+ <span data-ttu-id="efc63-195">**Full** bundles, indicated by the keyword `all`</span><span class="sxs-lookup"><span data-stu-id="efc63-195">**Full** bundles, indicated by the keyword `all`</span></span>
+ <span data-ttu-id="efc63-196">**Filtered** bundles, indicated by the keyword `where`, followed by a predicate expression</span><span class="sxs-lookup"><span data-stu-id="efc63-196">**Filtered** bundles, indicated by the keyword `where`, followed by a predicate expression</span></span>
+ <span data-ttu-id="efc63-197">**Convolutional** bundles, indicated by the keyword `convolve`, followed by the convolution attributes</span><span class="sxs-lookup"><span data-stu-id="efc63-197">**Convolutional** bundles, indicated by the keyword `convolve`, followed by the convolution attributes</span></span>
+ <span data-ttu-id="efc63-198">**Pooling** bundles, indicated by the keywords **max pool** or **mean pool**</span><span class="sxs-lookup"><span data-stu-id="efc63-198">**Pooling** bundles, indicated by the keywords **max pool** or **mean pool**</span></span>
+ <span data-ttu-id="efc63-199">**Response normalization** bundles, indicated by the keyword **response norm**</span><span class="sxs-lookup"><span data-stu-id="efc63-199">**Response normalization** bundles, indicated by the keyword **response norm**</span></span>

## <a name="full-bundles"></a><span data-ttu-id="efc63-200">Full bundles</span><span class="sxs-lookup"><span data-stu-id="efc63-200">Full bundles</span></span>

<span data-ttu-id="efc63-201">A full connection bundle includes a connection from each node in the source layer to each node in the destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-201">A full connection bundle includes a connection from each node in the source layer to each node in the destination layer.</span></span> <span data-ttu-id="efc63-202">This is the default network connection type.</span><span class="sxs-lookup"><span data-stu-id="efc63-202">This is the default network connection type.</span></span>

## <a name="filtered-bundles"></a><span data-ttu-id="efc63-203">Filtered bundles</span><span class="sxs-lookup"><span data-stu-id="efc63-203">Filtered bundles</span></span>

<span data-ttu-id="efc63-204">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span><span class="sxs-lookup"><span data-stu-id="efc63-204">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span></span> <span data-ttu-id="efc63-205">The following example defines two filtered bundles:</span><span class="sxs-lookup"><span data-stu-id="efc63-205">The following example defines two filtered bundles:</span></span>

```Net#
input Pixels [10, 20];
hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  
```

+ <span data-ttu-id="efc63-206">In the predicate for `ByRow`, `s` is a parameter representing an index into the rectangular array of nodes of the input layer, `Pixels`, and `d` is a parameter representing an index into the array of nodes of the hidden layer, `ByRow`.</span><span class="sxs-lookup"><span data-stu-id="efc63-206">In the predicate for `ByRow`, `s` is a parameter representing an index into the rectangular array of nodes of the input layer, `Pixels`, and `d` is a parameter representing an index into the array of nodes of the hidden layer, `ByRow`.</span></span> <span data-ttu-id="efc63-207">The type of both `s` and `d` is a tuple of integers of length two.</span><span class="sxs-lookup"><span data-stu-id="efc63-207">The type of both `s` and `d` is a tuple of integers of length two.</span></span> <span data-ttu-id="efc63-208">Conceptually, `s` ranges over all pairs of integers with `0 <= s[0] < 10` and `0 <= s[1] < 20`, and `d` ranges over all pairs of integers, with `0 <= d[0] < 10` and `0 <= d[1] < 12`.</span><span class="sxs-lookup"><span data-stu-id="efc63-208">Conceptually, `s` ranges over all pairs of integers with `0 <= s[0] < 10` and `0 <= s[1] < 20`, and `d` ranges over all pairs of integers, with `0 <= d[0] < 10` and `0 <= d[1] < 12`.</span></span> 

+ <span data-ttu-id="efc63-209">On the right-hand side of the predicate expression, there is a condition.</span><span class="sxs-lookup"><span data-stu-id="efc63-209">On the right-hand side of the predicate expression, there is a condition.</span></span> <span data-ttu-id="efc63-210">In this example, for every value of `s` and `d` such that the condition is True, there is an edge from the source layer node to the destination layer node.</span><span class="sxs-lookup"><span data-stu-id="efc63-210">In this example, for every value of `s` and `d` such that the condition is True, there is an edge from the source layer node to the destination layer node.</span></span> <span data-ttu-id="efc63-211">Thus, this filter expression indicates that the bundle includes a connection from the node defined by `s` to the node defined by `d` in all cases where s[0] is equal to d[0].</span><span class="sxs-lookup"><span data-stu-id="efc63-211">Thus, this filter expression indicates that the bundle includes a connection from the node defined by `s` to the node defined by `d` in all cases where s[0] is equal to d[0].</span></span>

<span data-ttu-id="efc63-212">Optionally, you can specify a set of weights for a filtered bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-212">Optionally, you can specify a set of weights for a filtered bundle.</span></span> <span data-ttu-id="efc63-213">The value for the **Weights** attribute must be a tuple of floating point values with a length that matches the number of connections defined by the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-213">The value for the **Weights** attribute must be a tuple of floating point values with a length that matches the number of connections defined by the bundle.</span></span> <span data-ttu-id="efc63-214">By default, weights are randomly generated.</span><span class="sxs-lookup"><span data-stu-id="efc63-214">By default, weights are randomly generated.</span></span>

<span data-ttu-id="efc63-215">Weight values are grouped by the destination node index.</span><span class="sxs-lookup"><span data-stu-id="efc63-215">Weight values are grouped by the destination node index.</span></span> <span data-ttu-id="efc63-216">That is, if the first destination node is connected to K source nodes, the first `K` elements of the **Weights** tuple are the weights for the first destination node, in source index order.</span><span class="sxs-lookup"><span data-stu-id="efc63-216">That is, if the first destination node is connected to K source nodes, the first `K` elements of the **Weights** tuple are the weights for the first destination node, in source index order.</span></span> <span data-ttu-id="efc63-217">The same applies for the remaining destination nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-217">The same applies for the remaining destination nodes.</span></span>

<span data-ttu-id="efc63-218">It's possible to specify weights directly as constant values.</span><span class="sxs-lookup"><span data-stu-id="efc63-218">It's possible to specify weights directly as constant values.</span></span> <span data-ttu-id="efc63-219">For example, if you learned the weights previously, you can specify them as constants using this syntax:</span><span class="sxs-lookup"><span data-stu-id="efc63-219">For example, if you learned the weights previously, you can specify them as constants using this syntax:</span></span>

`const Weights_1 = [0.0188045055, 0.130500451, ...]`

## <a name="convolutional-bundles"></a><span data-ttu-id="efc63-220">Convolutional bundles</span><span class="sxs-lookup"><span data-stu-id="efc63-220">Convolutional bundles</span></span>

<span data-ttu-id="efc63-221">When the training data has a homogeneous structure, convolutional connections are commonly used to learn high-level features of the data.</span><span class="sxs-lookup"><span data-stu-id="efc63-221">When the training data has a homogeneous structure, convolutional connections are commonly used to learn high-level features of the data.</span></span> <span data-ttu-id="efc63-222">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span><span class="sxs-lookup"><span data-stu-id="efc63-222">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span></span>  

<span data-ttu-id="efc63-223">Convolutional bundles employ rectangular **kernels** that are slid through the dimensions.</span><span class="sxs-lookup"><span data-stu-id="efc63-223">Convolutional bundles employ rectangular **kernels** that are slid through the dimensions.</span></span> <span data-ttu-id="efc63-224">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred to as **kernel applications**.</span><span class="sxs-lookup"><span data-stu-id="efc63-224">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred to as **kernel applications**.</span></span> <span data-ttu-id="efc63-225">Each kernel application corresponds to a node in the source layer, which is referred to as the **central node**.</span><span class="sxs-lookup"><span data-stu-id="efc63-225">Each kernel application corresponds to a node in the source layer, which is referred to as the **central node**.</span></span> <span data-ttu-id="efc63-226">The weights of a kernel are shared among many connections.</span><span class="sxs-lookup"><span data-stu-id="efc63-226">The weights of a kernel are shared among many connections.</span></span> <span data-ttu-id="efc63-227">In a convolutional bundle, each kernel is rectangular and all kernel applications are the same size.</span><span class="sxs-lookup"><span data-stu-id="efc63-227">In a convolutional bundle, each kernel is rectangular and all kernel applications are the same size.</span></span>  

<span data-ttu-id="efc63-228">Convolutional bundles support the following attributes:</span><span class="sxs-lookup"><span data-stu-id="efc63-228">Convolutional bundles support the following attributes:</span></span>

<span data-ttu-id="efc63-229">**InputShape** defines the dimensionality of the source layer for the purposes of this convolutional bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-229">**InputShape** defines the dimensionality of the source layer for the purposes of this convolutional bundle.</span></span> <span data-ttu-id="efc63-230">The value must be a tuple of positive integers.</span><span class="sxs-lookup"><span data-stu-id="efc63-230">The value must be a tuple of positive integers.</span></span> <span data-ttu-id="efc63-231">The product of the integers must equal the number of nodes in the source layer, but otherwise, it does not need to match the dimensionality declared for the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-231">The product of the integers must equal the number of nodes in the source layer, but otherwise, it does not need to match the dimensionality declared for the source layer.</span></span> <span data-ttu-id="efc63-232">The length of this tuple becomes the **arity** value for the convolutional bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-232">The length of this tuple becomes the **arity** value for the convolutional bundle.</span></span> <span data-ttu-id="efc63-233">Typically arity refers to the number of arguments or operands that a function can take.</span><span class="sxs-lookup"><span data-stu-id="efc63-233">Typically arity refers to the number of arguments or operands that a function can take.</span></span>

<span data-ttu-id="efc63-234">To define the shape and locations of the kernels, use the attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span><span class="sxs-lookup"><span data-stu-id="efc63-234">To define the shape and locations of the kernels, use the attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span></span>   

+ <span data-ttu-id="efc63-235">**KernelShape**: (required) Defines the dimensionality of each kernel for the convolutional bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-235">**KernelShape**: (required) Defines the dimensionality of each kernel for the convolutional bundle.</span></span> <span data-ttu-id="efc63-236">The value must be a tuple of positive integers with a length that equals the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-236">The value must be a tuple of positive integers with a length that equals the arity of the bundle.</span></span> <span data-ttu-id="efc63-237">Each component of this tuple must be no greater than the corresponding component of **InputShape**.</span><span class="sxs-lookup"><span data-stu-id="efc63-237">Each component of this tuple must be no greater than the corresponding component of **InputShape**.</span></span> 

+ <span data-ttu-id="efc63-238">**Stride**: (optional) Defines the sliding step sizes of the convolution (one step size for each dimension), that is the distance between the central nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-238">**Stride**: (optional) Defines the sliding step sizes of the convolution (one step size for each dimension), that is the distance between the central nodes.</span></span> <span data-ttu-id="efc63-239">The value must be a tuple of positive integers with a length that is the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-239">The value must be a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="efc63-240">Each component of this tuple must be no greater than the corresponding component of **KernelShape**.</span><span class="sxs-lookup"><span data-stu-id="efc63-240">Each component of this tuple must be no greater than the corresponding component of **KernelShape**.</span></span> <span data-ttu-id="efc63-241">The default value is a tuple with all components equal to one.</span><span class="sxs-lookup"><span data-stu-id="efc63-241">The default value is a tuple with all components equal to one.</span></span> 

+ <span data-ttu-id="efc63-242">**Sharing**: (optional) Defines the weight sharing for each dimension of the convolution.</span><span class="sxs-lookup"><span data-stu-id="efc63-242">**Sharing**: (optional) Defines the weight sharing for each dimension of the convolution.</span></span> <span data-ttu-id="efc63-243">The value can be a single Boolean value or a tuple of Boolean values with a length that is the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-243">The value can be a single Boolean value or a tuple of Boolean values with a length that is the arity of the bundle.</span></span> <span data-ttu-id="efc63-244">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span><span class="sxs-lookup"><span data-stu-id="efc63-244">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> <span data-ttu-id="efc63-245">The default value is a tuple that consists of all True values.</span><span class="sxs-lookup"><span data-stu-id="efc63-245">The default value is a tuple that consists of all True values.</span></span> 

+ <span data-ttu-id="efc63-246">**MapCount**: (optional) Defines the number of feature maps for the convolutional bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-246">**MapCount**: (optional) Defines the number of feature maps for the convolutional bundle.</span></span> <span data-ttu-id="efc63-247">The value can be a single positive integer or a tuple of positive integers with a length that is the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-247">The value can be a single positive integer or a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="efc63-248">A single integer value is extended to be a tuple of the correct length with the first components equal to the specified value and all the remaining components equal to one.</span><span class="sxs-lookup"><span data-stu-id="efc63-248">A single integer value is extended to be a tuple of the correct length with the first components equal to the specified value and all the remaining components equal to one.</span></span> <span data-ttu-id="efc63-249">The default value is one.</span><span class="sxs-lookup"><span data-stu-id="efc63-249">The default value is one.</span></span> <span data-ttu-id="efc63-250">The total number of feature maps is the product of the components of the tuple.</span><span class="sxs-lookup"><span data-stu-id="efc63-250">The total number of feature maps is the product of the components of the tuple.</span></span> <span data-ttu-id="efc63-251">The factoring of this total number across the components determines how the feature map values are grouped in the destination nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-251">The factoring of this total number across the components determines how the feature map values are grouped in the destination nodes.</span></span> 

+ <span data-ttu-id="efc63-252">**Weights**: (optional) Defines the initial weights for the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-252">**Weights**: (optional) Defines the initial weights for the bundle.</span></span> <span data-ttu-id="efc63-253">The value must be a tuple of floating point values with a length that is the number of kernels times the number of weights per kernel, as defined later in this article.</span><span class="sxs-lookup"><span data-stu-id="efc63-253">The value must be a tuple of floating point values with a length that is the number of kernels times the number of weights per kernel, as defined later in this article.</span></span> <span data-ttu-id="efc63-254">The default weights are randomly generated.</span><span class="sxs-lookup"><span data-stu-id="efc63-254">The default weights are randomly generated.</span></span>  

<span data-ttu-id="efc63-255">There are two sets of properties that control padding, the properties being mutually exclusive:</span><span class="sxs-lookup"><span data-stu-id="efc63-255">There are two sets of properties that control padding, the properties being mutually exclusive:</span></span>

+ <span data-ttu-id="efc63-256">**Padding**: (optional) Determines whether the input should be padded by using a **default padding scheme**.</span><span class="sxs-lookup"><span data-stu-id="efc63-256">**Padding**: (optional) Determines whether the input should be padded by using a **default padding scheme**.</span></span> <span data-ttu-id="efc63-257">The value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-257">The value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is the arity of the bundle.</span></span> 

    <span data-ttu-id="efc63-258">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span><span class="sxs-lookup"><span data-stu-id="efc63-258">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> 
    
    <span data-ttu-id="efc63-259">If the value for a dimension is True, the source is logically padded in that dimension with zero-valued cells to support additional kernel applications, such that the central nodes of the first and last kernels in that dimension are the first and last nodes in that dimension in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-259">If the value for a dimension is True, the source is logically padded in that dimension with zero-valued cells to support additional kernel applications, such that the central nodes of the first and last kernels in that dimension are the first and last nodes in that dimension in the source layer.</span></span> <span data-ttu-id="efc63-260">Thus, the number of "dummy" nodes in each dimension is determined automatically, to fit exactly `(InputShape[d] - 1) / Stride[d] + 1` kernels into the padded source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-260">Thus, the number of "dummy" nodes in each dimension is determined automatically, to fit exactly `(InputShape[d] - 1) / Stride[d] + 1` kernels into the padded source layer.</span></span> 
    
    <span data-ttu-id="efc63-261">If the value for a dimension is False, the kernels are defined so that the number of nodes on each side that are left out is the same (up to a difference of 1).</span><span class="sxs-lookup"><span data-stu-id="efc63-261">If the value for a dimension is False, the kernels are defined so that the number of nodes on each side that are left out is the same (up to a difference of 1).</span></span> <span data-ttu-id="efc63-262">The default value of this attribute is a tuple with all components equal to False.</span><span class="sxs-lookup"><span data-stu-id="efc63-262">The default value of this attribute is a tuple with all components equal to False.</span></span>

+ <span data-ttu-id="efc63-263">**UpperPad** and **LowerPad**: (optional) Provide greater control over the amount of padding to use.</span><span class="sxs-lookup"><span data-stu-id="efc63-263">**UpperPad** and **LowerPad**: (optional) Provide greater control over the amount of padding to use.</span></span> <span data-ttu-id="efc63-264">**Important:** These attributes can be defined if and only if the **Padding** property above is ***not*** defined.</span><span class="sxs-lookup"><span data-stu-id="efc63-264">**Important:** These attributes can be defined if and only if the **Padding** property above is ***not*** defined.</span></span> <span data-ttu-id="efc63-265">The values should be integer-valued tuples with lengths that are the arity of the bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-265">The values should be integer-valued tuples with lengths that are the arity of the bundle.</span></span> <span data-ttu-id="efc63-266">When these attributes are specified, "dummy" nodes are added to the lower and upper ends of each dimension of the input layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-266">When these attributes are specified, "dummy" nodes are added to the lower and upper ends of each dimension of the input layer.</span></span> <span data-ttu-id="efc63-267">The number of nodes added to the lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span><span class="sxs-lookup"><span data-stu-id="efc63-267">The number of nodes added to the lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span></span> 

    <span data-ttu-id="efc63-268">To ensure that kernels correspond only to "real" nodes and not to "dummy" nodes, the following conditions must be met:</span><span class="sxs-lookup"><span data-stu-id="efc63-268">To ensure that kernels correspond only to "real" nodes and not to "dummy" nodes, the following conditions must be met:</span></span>
      - <span data-ttu-id="efc63-269">Each component of **LowerPad** must be strictly less than `KernelShape[d]/2`.</span><span class="sxs-lookup"><span data-stu-id="efc63-269">Each component of **LowerPad** must be strictly less than `KernelShape[d]/2`.</span></span> 
      - <span data-ttu-id="efc63-270">Each component of **UpperPad** must be no greater than `KernelShape[d]/2`.</span><span class="sxs-lookup"><span data-stu-id="efc63-270">Each component of **UpperPad** must be no greater than `KernelShape[d]/2`.</span></span> 
      - <span data-ttu-id="efc63-271">The default value of these attributes is a tuple with all components equal to 0.</span><span class="sxs-lookup"><span data-stu-id="efc63-271">The default value of these attributes is a tuple with all components equal to 0.</span></span> 

    <span data-ttu-id="efc63-272">The setting **Padding** = true allows as much padding as is needed to keep the "center" of the kernel inside the "real" input.</span><span class="sxs-lookup"><span data-stu-id="efc63-272">The setting **Padding** = true allows as much padding as is needed to keep the "center" of the kernel inside the "real" input.</span></span> <span data-ttu-id="efc63-273">This changes the math a bit for computing the output size.</span><span class="sxs-lookup"><span data-stu-id="efc63-273">This changes the math a bit for computing the output size.</span></span> <span data-ttu-id="efc63-274">Generally, the output size *D* is computed as `D = (I - K) / S + 1`, where `I` is the input size, `K` is the kernel size, `S` is the stride, and `/` is integer division (round toward zero).</span><span class="sxs-lookup"><span data-stu-id="efc63-274">Generally, the output size *D* is computed as `D = (I - K) / S + 1`, where `I` is the input size, `K` is the kernel size, `S` is the stride, and `/` is integer division (round toward zero).</span></span> <span data-ttu-id="efc63-275">If you set UpperPad = [1, 1], the input size `I` is effectively 29, and thus `D = (29 - 5) / 2 + 1 = 13`.</span><span class="sxs-lookup"><span data-stu-id="efc63-275">If you set UpperPad = [1, 1], the input size `I` is effectively 29, and thus `D = (29 - 5) / 2 + 1 = 13`.</span></span> <span data-ttu-id="efc63-276">However, when **Padding** = true, essentially `I` gets bumped up by `K - 1`; hence `D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14`.</span><span class="sxs-lookup"><span data-stu-id="efc63-276">However, when **Padding** = true, essentially `I` gets bumped up by `K - 1`; hence `D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14`.</span></span> <span data-ttu-id="efc63-277">By specifying values for **UpperPad** and **LowerPad** you get much more control over the padding than if you just set **Padding** = true.</span><span class="sxs-lookup"><span data-stu-id="efc63-277">By specifying values for **UpperPad** and **LowerPad** you get much more control over the padding than if you just set **Padding** = true.</span></span>

<span data-ttu-id="efc63-278">For more information about convolutional networks and their applications, see these articles:</span><span class="sxs-lookup"><span data-stu-id="efc63-278">For more information about convolutional networks and their applications, see these articles:</span></span> 

+ [<span data-ttu-id="efc63-279">http://deeplearning.net/tutorial/lenet.html </span><span class="sxs-lookup"><span data-stu-id="efc63-279">http://deeplearning.net/tutorial/lenet.html </span></span>](http://deeplearning.net/tutorial/lenet.html)
+ [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
+ [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a><span data-ttu-id="efc63-280">Pooling bundles</span><span class="sxs-lookup"><span data-stu-id="efc63-280">Pooling bundles</span></span>

<span data-ttu-id="efc63-281">A **pooling bundle** applies geometry similar to convolutional connectivity, but it uses predefined functions to source node values to derive the destination node value.</span><span class="sxs-lookup"><span data-stu-id="efc63-281">A **pooling bundle** applies geometry similar to convolutional connectivity, but it uses predefined functions to source node values to derive the destination node value.</span></span> <span data-ttu-id="efc63-282">Hence, pooling bundles have no trainable state (weights or biases).</span><span class="sxs-lookup"><span data-stu-id="efc63-282">Hence, pooling bundles have no trainable state (weights or biases).</span></span> <span data-ttu-id="efc63-283">Pooling bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span><span class="sxs-lookup"><span data-stu-id="efc63-283">Pooling bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>

<span data-ttu-id="efc63-284">Typically, the kernels summarized by adjacent pooling units do not overlap.</span><span class="sxs-lookup"><span data-stu-id="efc63-284">Typically, the kernels summarized by adjacent pooling units do not overlap.</span></span> <span data-ttu-id="efc63-285">If Stride[d] is equal to KernelShape[d] in each dimension, the layer obtained is the traditional local pooling layer, which is commonly employed in convolutional neural networks.</span><span class="sxs-lookup"><span data-stu-id="efc63-285">If Stride[d] is equal to KernelShape[d] in each dimension, the layer obtained is the traditional local pooling layer, which is commonly employed in convolutional neural networks.</span></span> <span data-ttu-id="efc63-286">Each destination node computes the maximum or the mean of the activities of its kernel in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-286">Each destination node computes the maximum or the mean of the activities of its kernel in the source layer.</span></span>  

<span data-ttu-id="efc63-287">The following example illustrates a pooling bundle:</span><span class="sxs-lookup"><span data-stu-id="efc63-287">The following example illustrates a pooling bundle:</span></span> 

```Net#
hidden P1 [5, 12, 12]
  from C1 max pool {
  InputShape  = [ 5, 24, 24];
   KernelShape = [ 1,  2,  2];
   Stride      = [ 1,  2,  2];
  }  
```

+ <span data-ttu-id="efc63-288">The arity of the bundle is 3: that is, the length of the tuples `InputShape`, `KernelShape`, and `Stride`.</span><span class="sxs-lookup"><span data-stu-id="efc63-288">The arity of the bundle is 3: that is, the length of the tuples `InputShape`, `KernelShape`, and `Stride`.</span></span> 
+ <span data-ttu-id="efc63-289">The number of nodes in the source layer is `5 * 24 * 24 = 2880`.</span><span class="sxs-lookup"><span data-stu-id="efc63-289">The number of nodes in the source layer is `5 * 24 * 24 = 2880`.</span></span> 
+ <span data-ttu-id="efc63-290">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span><span class="sxs-lookup"><span data-stu-id="efc63-290">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span></span> 
+ <span data-ttu-id="efc63-291">The number of nodes in the destination layer is `5 * 12 * 12 = 1440`.</span><span class="sxs-lookup"><span data-stu-id="efc63-291">The number of nodes in the destination layer is `5 * 12 * 12 = 1440`.</span></span>

<span data-ttu-id="efc63-292">For more information about pooling layers, see these articles:</span><span class="sxs-lookup"><span data-stu-id="efc63-292">For more information about pooling layers, see these articles:</span></span>  

+ <span data-ttu-id="efc63-293">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span><span class="sxs-lookup"><span data-stu-id="efc63-293">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span></span>
+ [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
+ [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a><span data-ttu-id="efc63-294">Response normalization bundles</span><span class="sxs-lookup"><span data-stu-id="efc63-294">Response normalization bundles</span></span>

<span data-ttu-id="efc63-295">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in the paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span><span class="sxs-lookup"><span data-stu-id="efc63-295">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in the paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span></span> 

<span data-ttu-id="efc63-296">Response normalization is used to aid generalization in neural nets.</span><span class="sxs-lookup"><span data-stu-id="efc63-296">Response normalization is used to aid generalization in neural nets.</span></span> <span data-ttu-id="efc63-297">When one neuron is firing at a very high activation level, a local response normalization layer suppresses the activation level of the surrounding neurons.</span><span class="sxs-lookup"><span data-stu-id="efc63-297">When one neuron is firing at a very high activation level, a local response normalization layer suppresses the activation level of the surrounding neurons.</span></span> <span data-ttu-id="efc63-298">This is done by using three parameters (`α`, `β`, and `k`) and a convolutional structure (or neighborhood shape).</span><span class="sxs-lookup"><span data-stu-id="efc63-298">This is done by using three parameters (`α`, `β`, and `k`) and a convolutional structure (or neighborhood shape).</span></span> <span data-ttu-id="efc63-299">Every neuron in the destination layer **y** corresponds to a neuron **x** in the source layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-299">Every neuron in the destination layer **y** corresponds to a neuron **x** in the source layer.</span></span> <span data-ttu-id="efc63-300">The activation level of **y** is given by the following formula, where `f` is the activation level of a neuron, and `Nx` is the kernel (or the set that contains the neurons in the neighborhood of **x**), as defined by the following convolutional structure:</span><span class="sxs-lookup"><span data-stu-id="efc63-300">The activation level of **y** is given by the following formula, where `f` is the activation level of a neuron, and `Nx` is the kernel (or the set that contains the neurons in the neighborhood of **x**), as defined by the following convolutional structure:</span></span>  

![formula for convolutional structure](./media/azure-ml-netsharp-reference-guide/formula_large.png)

<span data-ttu-id="efc63-302">Response normalization bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span><span class="sxs-lookup"><span data-stu-id="efc63-302">Response normalization bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

+ <span data-ttu-id="efc63-303">If the kernel contains neurons in the same map as ***x***, the normalization scheme is referred to as **same map normalization**.</span><span class="sxs-lookup"><span data-stu-id="efc63-303">If the kernel contains neurons in the same map as ***x***, the normalization scheme is referred to as **same map normalization**.</span></span> <span data-ttu-id="efc63-304">To define same map normalization, the first coordinate in **InputShape** must have the value 1.</span><span class="sxs-lookup"><span data-stu-id="efc63-304">To define same map normalization, the first coordinate in **InputShape** must have the value 1.</span></span>

+ <span data-ttu-id="efc63-305">If the kernel contains neurons in the same spatial position as ***x***, but the neurons are in other maps, the normalization scheme is called **across maps normalization**.</span><span class="sxs-lookup"><span data-stu-id="efc63-305">If the kernel contains neurons in the same spatial position as ***x***, but the neurons are in other maps, the normalization scheme is called **across maps normalization**.</span></span> <span data-ttu-id="efc63-306">This type of response normalization implements a form of lateral inhibition inspired by the type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span><span class="sxs-lookup"><span data-stu-id="efc63-306">This type of response normalization implements a form of lateral inhibition inspired by the type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span></span> <span data-ttu-id="efc63-307">To define across maps normalization, the first coordinate must be an integer greater than one and no greater than the number of maps, and the rest of the coordinates must have the value 1.</span><span class="sxs-lookup"><span data-stu-id="efc63-307">To define across maps normalization, the first coordinate must be an integer greater than one and no greater than the number of maps, and the rest of the coordinates must have the value 1.</span></span>

<span data-ttu-id="efc63-308">Because response normalization bundles apply a predefined function to source node values to determine the destination node value, they have no trainable state (weights or biases).</span><span class="sxs-lookup"><span data-stu-id="efc63-308">Because response normalization bundles apply a predefined function to source node values to determine the destination node value, they have no trainable state (weights or biases).</span></span>

> [!NOTE]
> <span data-ttu-id="efc63-309">The nodes in the destination layer correspond to neurons that are the central nodes of the kernels.</span><span class="sxs-lookup"><span data-stu-id="efc63-309">The nodes in the destination layer correspond to neurons that are the central nodes of the kernels.</span></span> <span data-ttu-id="efc63-310">For example, if `KernelShape[d]` is odd, then `KernelShape[d]/2` corresponds to the central kernel node.</span><span class="sxs-lookup"><span data-stu-id="efc63-310">For example, if `KernelShape[d]` is odd, then `KernelShape[d]/2` corresponds to the central kernel node.</span></span> <span data-ttu-id="efc63-311">If `KernelShape[d]` is even, the central node is at `KernelShape[d]/2 - 1`.</span><span class="sxs-lookup"><span data-stu-id="efc63-311">If `KernelShape[d]` is even, the central node is at `KernelShape[d]/2 - 1`.</span></span> <span data-ttu-id="efc63-312">Therefore, if `Padding[d]` is False, the first and the last `KernelShape[d]/2` nodes do not have corresponding nodes in the destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-312">Therefore, if `Padding[d]` is False, the first and the last `KernelShape[d]/2` nodes do not have corresponding nodes in the destination layer.</span></span> <span data-ttu-id="efc63-313">To avoid this situation, define **Padding** as [true, true, …, true].</span><span class="sxs-lookup"><span data-stu-id="efc63-313">To avoid this situation, define **Padding** as [true, true, …, true].</span></span>

<span data-ttu-id="efc63-314">In addition to the four attributes described earlier, response normalization bundles also support the following attributes:</span><span class="sxs-lookup"><span data-stu-id="efc63-314">In addition to the four attributes described earlier, response normalization bundles also support the following attributes:</span></span>

+ <span data-ttu-id="efc63-315">**Alpha**: (required) Specifies a floating-point value that corresponds to `α` in the previous formula.</span><span class="sxs-lookup"><span data-stu-id="efc63-315">**Alpha**: (required) Specifies a floating-point value that corresponds to `α` in the previous formula.</span></span> 
+ <span data-ttu-id="efc63-316">**Beta**: (required) Specifies a floating-point value that corresponds to `β` in the previous formula.</span><span class="sxs-lookup"><span data-stu-id="efc63-316">**Beta**: (required) Specifies a floating-point value that corresponds to `β` in the previous formula.</span></span> 
+ <span data-ttu-id="efc63-317">**Offset**: (optional) Specifies a floating-point value that corresponds to `k` in the previous formula.</span><span class="sxs-lookup"><span data-stu-id="efc63-317">**Offset**: (optional) Specifies a floating-point value that corresponds to `k` in the previous formula.</span></span> <span data-ttu-id="efc63-318">It defaults to 1.</span><span class="sxs-lookup"><span data-stu-id="efc63-318">It defaults to 1.</span></span>

<span data-ttu-id="efc63-319">The following example defines a response normalization bundle using these attributes:</span><span class="sxs-lookup"><span data-stu-id="efc63-319">The following example defines a response normalization bundle using these attributes:</span></span>  

```Net#
hidden RN1 [5, 10, 10]
from P1 response norm {
  InputShape  = [ 5, 12, 12];
  KernelShape = [ 1,  3,  3];
  Alpha = 0.001;
  Beta = 0.75;
  }  
```

+ <span data-ttu-id="efc63-320">The source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-320">The source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span></span> 
+ <span data-ttu-id="efc63-321">The value of **KernelShape** indicates that this is a same map normalization layer, where the neighborhood is a 3x3 rectangle.</span><span class="sxs-lookup"><span data-stu-id="efc63-321">The value of **KernelShape** indicates that this is a same map normalization layer, where the neighborhood is a 3x3 rectangle.</span></span> 
+ <span data-ttu-id="efc63-322">The default value of **Padding** is False, thus the destination layer has only 10 nodes in each dimension.</span><span class="sxs-lookup"><span data-stu-id="efc63-322">The default value of **Padding** is False, thus the destination layer has only 10 nodes in each dimension.</span></span> <span data-ttu-id="efc63-323">To include one node in the destination layer that corresponds to every node in the source layer, add Padding = [true, true, true]; and change the size of RN1 to [5, 12, 12].</span><span class="sxs-lookup"><span data-stu-id="efc63-323">To include one node in the destination layer that corresponds to every node in the source layer, add Padding = [true, true, true]; and change the size of RN1 to [5, 12, 12].</span></span>  

## <a name="share-declaration"></a><span data-ttu-id="efc63-324">Share declaration</span><span class="sxs-lookup"><span data-stu-id="efc63-324">Share declaration</span></span>

<span data-ttu-id="efc63-325">Net# optionally supports defining multiple bundles with shared weights.</span><span class="sxs-lookup"><span data-stu-id="efc63-325">Net# optionally supports defining multiple bundles with shared weights.</span></span> <span data-ttu-id="efc63-326">The weights of any two bundles can be shared if their structures are the same.</span><span class="sxs-lookup"><span data-stu-id="efc63-326">The weights of any two bundles can be shared if their structures are the same.</span></span> <span data-ttu-id="efc63-327">The following syntax defines bundles with shared weights:</span><span class="sxs-lookup"><span data-stu-id="efc63-327">The following syntax defines bundles with shared weights:</span></span>  

```Net#
share-declaration:
  share    {    layer-list    }
  share    {    bundle-list    }
  share    {    bias-list    }

  layer-list:
    layer-name    ,    layer-name
    layer-list    ,    layer-name

  bundle-list:
    bundle-spec    ,    bundle-spec
    bundle-list    ,    bundle-spec

  bundle-spec:
    layer-name    =>     layer-name

  bias-list:
    bias-spec    ,    bias-spec
    bias-list    ,    bias-spec

  bias-spec:
    1    =>    layer-name

  layer-name:
    identifier
```

<span data-ttu-id="efc63-328">For example, the following share-declaration specifies the layer names, indicating that both weights and biases should be shared:</span><span class="sxs-lookup"><span data-stu-id="efc63-328">For example, the following share-declaration specifies the layer names, indicating that both weights and biases should be shared:</span></span>  

```Net#
Const {
  InputSize = 37;
  HiddenSize = 50;
  }
input {
  Data1 [InputSize];
  Data2 [InputSize];
  }
hidden {
  H1 [HiddenSize] from Data1 all;
  H2 [HiddenSize] from Data2 all;
  }
output Result [2] {
  from H1 all;
  from H2 all;
  }
share { H1, H2 } // share both weights and biases  
```

+ <span data-ttu-id="efc63-329">The input features are partitioned into two equal sized input layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-329">The input features are partitioned into two equal sized input layers.</span></span> 
+ <span data-ttu-id="efc63-330">The hidden layers then compute higher level features on the two input layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-330">The hidden layers then compute higher level features on the two input layers.</span></span> 
+ <span data-ttu-id="efc63-331">The share-declaration specifies that *H1* and *H2* must be computed in the same way from their respective inputs.</span><span class="sxs-lookup"><span data-stu-id="efc63-331">The share-declaration specifies that *H1* and *H2* must be computed in the same way from their respective inputs.</span></span>  

<span data-ttu-id="efc63-332">Alternatively, this could be specified with two separate share-declarations as follows:</span><span class="sxs-lookup"><span data-stu-id="efc63-332">Alternatively, this could be specified with two separate share-declarations as follows:</span></span>  

```Net#
share { Data1 => H1, Data2 => H2 } // share weights  
<!-- -->
    share { 1 => H1, 1 => H2 } // share biases  
```

<span data-ttu-id="efc63-333">You can use the short form only when the layers contain a single bundle.</span><span class="sxs-lookup"><span data-stu-id="efc63-333">You can use the short form only when the layers contain a single bundle.</span></span> <span data-ttu-id="efc63-334">In general, sharing is possible only when the relevant structure is identical, meaning that they have the same size, same convolutional geometry, and so forth.</span><span class="sxs-lookup"><span data-stu-id="efc63-334">In general, sharing is possible only when the relevant structure is identical, meaning that they have the same size, same convolutional geometry, and so forth.</span></span>  

## <a name="examples-of-net-usage"></a><span data-ttu-id="efc63-335">Examples of Net# usage</span><span class="sxs-lookup"><span data-stu-id="efc63-335">Examples of Net# usage</span></span>

<span data-ttu-id="efc63-336">This section provides some examples of how you can use Net# to add hidden layers, define the way that hidden layers interact with other layers, and build convolutional networks.</span><span class="sxs-lookup"><span data-stu-id="efc63-336">This section provides some examples of how you can use Net# to add hidden layers, define the way that hidden layers interact with other layers, and build convolutional networks.</span></span>

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a><span data-ttu-id="efc63-337">Define a simple custom neural network: "Hello World" example</span><span class="sxs-lookup"><span data-stu-id="efc63-337">Define a simple custom neural network: "Hello World" example</span></span>

<span data-ttu-id="efc63-338">This simple example demonstrates how to create a neural network model that has a single hidden layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-338">This simple example demonstrates how to create a neural network model that has a single hidden layer.</span></span>

```Net#
input Data auto;
hidden H [200] from Data all;
output Out [10] sigmoid from H all;  
```

<span data-ttu-id="efc63-339">The example illustrates some basic commands as follows:</span><span class="sxs-lookup"><span data-stu-id="efc63-339">The example illustrates some basic commands as follows:</span></span>  

+ <span data-ttu-id="efc63-340">The first line defines the input layer (named `Data`).</span><span class="sxs-lookup"><span data-stu-id="efc63-340">The first line defines the input layer (named `Data`).</span></span> <span data-ttu-id="efc63-341">When you use the  `auto` keyword, the neural network automatically includes all feature columns in the input examples.</span><span class="sxs-lookup"><span data-stu-id="efc63-341">When you use the  `auto` keyword, the neural network automatically includes all feature columns in the input examples.</span></span> 
+ <span data-ttu-id="efc63-342">The second line creates the hidden layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-342">The second line creates the hidden layer.</span></span> <span data-ttu-id="efc63-343">The name `H` is assigned to the hidden layer, which has 200 nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-343">The name `H` is assigned to the hidden layer, which has 200 nodes.</span></span> <span data-ttu-id="efc63-344">This layer is fully connected to the input layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-344">This layer is fully connected to the input layer.</span></span>
+ <span data-ttu-id="efc63-345">The third line defines the output layer (named `O`), which contains 10 output nodes.</span><span class="sxs-lookup"><span data-stu-id="efc63-345">The third line defines the output layer (named `O`), which contains 10 output nodes.</span></span> <span data-ttu-id="efc63-346">If the neural network is used for classification, there is one output node per class.</span><span class="sxs-lookup"><span data-stu-id="efc63-346">If the neural network is used for classification, there is one output node per class.</span></span> <span data-ttu-id="efc63-347">The keyword **sigmoid** indicates that the output function is applied to the output layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-347">The keyword **sigmoid** indicates that the output function is applied to the output layer.</span></span>

### <a name="define-multiple-hidden-layers-computer-vision-example"></a><span data-ttu-id="efc63-348">Define multiple hidden layers: computer vision example</span><span class="sxs-lookup"><span data-stu-id="efc63-348">Define multiple hidden layers: computer vision example</span></span>

<span data-ttu-id="efc63-349">The following example demonstrates how to define a slightly more complex neural network, with multiple custom hidden layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-349">The following example demonstrates how to define a slightly more complex neural network, with multiple custom hidden layers.</span></span>  

```Net#
// Define the input layers 
input Pixels [10, 20];
input MetaData [7];

// Define the first two hidden layers, using data only from the Pixels input
hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

// Define the third hidden layer, which uses as source the hidden layers ByRow and ByCol
hidden Gather [100] 
{
from ByRow all;
from ByCol all;
}

// Define the output layer and its sources
output Result [10]  
{
from Gather all;
from MetaData all;
}  
```

<span data-ttu-id="efc63-350">This example illustrates several features of the neural networks specification language:</span><span class="sxs-lookup"><span data-stu-id="efc63-350">This example illustrates several features of the neural networks specification language:</span></span>

+ <span data-ttu-id="efc63-351">The structure has two input layers, `Pixels` and `MetaData`.</span><span class="sxs-lookup"><span data-stu-id="efc63-351">The structure has two input layers, `Pixels` and `MetaData`.</span></span>
+ <span data-ttu-id="efc63-352">The `Pixels` layer is a source layer for two connection bundles, with destination layers, `ByRow` and `ByCol`.</span><span class="sxs-lookup"><span data-stu-id="efc63-352">The `Pixels` layer is a source layer for two connection bundles, with destination layers, `ByRow` and `ByCol`.</span></span>
+ <span data-ttu-id="efc63-353">The layers `Gather` and `Result` are destination layers in multiple connection bundles.</span><span class="sxs-lookup"><span data-stu-id="efc63-353">The layers `Gather` and `Result` are destination layers in multiple connection bundles.</span></span>
+ <span data-ttu-id="efc63-354">The output layer, `Result`, is a destination layer in two connection bundles; one with the second level hidden layer `Gather` as a destination layer, and the other with the input layer `MetaData` as a destination layer.</span><span class="sxs-lookup"><span data-stu-id="efc63-354">The output layer, `Result`, is a destination layer in two connection bundles; one with the second level hidden layer `Gather` as a destination layer, and the other with the input layer `MetaData` as a destination layer.</span></span>
+ <span data-ttu-id="efc63-355">The hidden layers, `ByRow` and `ByCol`, specify filtered connectivity by using predicate expressions.</span><span class="sxs-lookup"><span data-stu-id="efc63-355">The hidden layers, `ByRow` and `ByCol`, specify filtered connectivity by using predicate expressions.</span></span> <span data-ttu-id="efc63-356">More precisely, the node in `ByRow` at [x, y] is connected to the nodes in `Pixels` that have the first index coordinate equal to the node's first coordinate, x.</span><span class="sxs-lookup"><span data-stu-id="efc63-356">More precisely, the node in `ByRow` at [x, y] is connected to the nodes in `Pixels` that have the first index coordinate equal to the node's first coordinate, x.</span></span> <span data-ttu-id="efc63-357">Similarly, the node in `ByCol` at [x, y] is connected to the nodes in `Pixels` that have the second index coordinate within one of the node's second coordinate, y.</span><span class="sxs-lookup"><span data-stu-id="efc63-357">Similarly, the node in `ByCol` at [x, y] is connected to the nodes in `Pixels` that have the second index coordinate within one of the node's second coordinate, y.</span></span>

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a><span data-ttu-id="efc63-358">Define a convolutional network for multiclass classification: digit recognition example</span><span class="sxs-lookup"><span data-stu-id="efc63-358">Define a convolutional network for multiclass classification: digit recognition example</span></span>

<span data-ttu-id="efc63-359">The definition of the following network is designed to recognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span><span class="sxs-lookup"><span data-stu-id="efc63-359">The definition of the following network is designed to recognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span></span>  

```Net#
input Image [29, 29];
hidden Conv1 [5, 13, 13] from Image convolve 
  {
  InputShape  = [29, 29];
  KernelShape = [ 5,  5];
  Stride      = [ 2,  2];
  MapCount    = 5;
  }
hidden Conv2 [50, 5, 5]
from Conv1 convolve 
  {
  InputShape  = [ 5, 13, 13];
  KernelShape = [ 1,  5,  5];
  Stride      = [ 1,  2,  2];
  Sharing     = [false, true, true];
  MapCount    = 10;
  }
hidden Hid3 [100] from Conv2 all;
output Digit [10] from Hid3 all;  
```

+ <span data-ttu-id="efc63-360">The structure has a single input layer, `Image`.</span><span class="sxs-lookup"><span data-stu-id="efc63-360">The structure has a single input layer, `Image`.</span></span>
+ <span data-ttu-id="efc63-361">The keyword `convolve` indicates that the layers named `Conv1` and `Conv2` are convolutional layers.</span><span class="sxs-lookup"><span data-stu-id="efc63-361">The keyword `convolve` indicates that the layers named `Conv1` and `Conv2` are convolutional layers.</span></span> <span data-ttu-id="efc63-362">Each of these layer declarations is followed by a list of the convolution attributes.</span><span class="sxs-lookup"><span data-stu-id="efc63-362">Each of these layer declarations is followed by a list of the convolution attributes.</span></span>
+ <span data-ttu-id="efc63-363">The net has a third hidden layer, `Hid3`, which is fully connected to the second hidden layer, `Conv2`.</span><span class="sxs-lookup"><span data-stu-id="efc63-363">The net has a third hidden layer, `Hid3`, which is fully connected to the second hidden layer, `Conv2`.</span></span>
+ <span data-ttu-id="efc63-364">The output layer, `Digit`, is connected only to the third hidden layer, `Hid3`.</span><span class="sxs-lookup"><span data-stu-id="efc63-364">The output layer, `Digit`, is connected only to the third hidden layer, `Hid3`.</span></span> <span data-ttu-id="efc63-365">The keyword `all` indicates that the output layer is fully connected to `Hid3`.</span><span class="sxs-lookup"><span data-stu-id="efc63-365">The keyword `all` indicates that the output layer is fully connected to `Hid3`.</span></span>
+ <span data-ttu-id="efc63-366">The arity of the convolution is three: the length of the tuples `InputShape`, `KernelShape`, `Stride, and `Sharing\`.</span><span class="sxs-lookup"><span data-stu-id="efc63-366">The arity of the convolution is three: the length of the tuples `InputShape`, `KernelShape`, `Stride, and `Sharing\`.</span></span> 
+ <span data-ttu-id="efc63-367">The number of weights per kernel is `1 + KernelShape\[0] * KernelShape\[1] * KernelShape\[2] = 1 + 1 * 5 * 5 = 26`.</span><span class="sxs-lookup"><span data-stu-id="efc63-367">The number of weights per kernel is `1 + KernelShape\[0] * KernelShape\[1] * KernelShape\[2] = 1 + 1 * 5 * 5 = 26`.</span></span> <span data-ttu-id="efc63-368">Or `26 * 50 = 1300`.</span><span class="sxs-lookup"><span data-stu-id="efc63-368">Or `26 * 50 = 1300`.</span></span>
+ <span data-ttu-id="efc63-369">You can calculate the nodes in each hidden layer as follows:</span><span class="sxs-lookup"><span data-stu-id="efc63-369">You can calculate the nodes in each hidden layer as follows:</span></span>

    <span data-ttu-id="efc63-370">`NodeCount\[0] = (5 - 1) / 1 + 1 = 5` `NodeCount\[1] = (13 - 5) / 2 + 1 = 5`</span><span class="sxs-lookup"><span data-stu-id="efc63-370">`NodeCount\[0] = (5 - 1) / 1 + 1 = 5` `NodeCount\[1] = (13 - 5) / 2 + 1 = 5`</span></span>
    `NodeCount\[2] = (13 - 5) / 2 + 1 = 5`

+ <span data-ttu-id="efc63-371">The total number of nodes can be calculated by using the declared dimensionality of the layer, [50, 5, 5], as follows: `MapCount * NodeCount\[0] * NodeCount\[1] * NodeCount\[2] = 10 * 5 * 5 * 5`</span><span class="sxs-lookup"><span data-stu-id="efc63-371">The total number of nodes can be calculated by using the declared dimensionality of the layer, [50, 5, 5], as follows: `MapCount * NodeCount\[0] * NodeCount\[1] * NodeCount\[2] = 10 * 5 * 5 * 5`</span></span>
+ <span data-ttu-id="efc63-372">Because `Sharing[d]` is False only for `d == 0`, the number of kernels is `MapCount * NodeCount\[0] = 10 * 5 = 50`.</span><span class="sxs-lookup"><span data-stu-id="efc63-372">Because `Sharing[d]` is False only for `d == 0`, the number of kernels is `MapCount * NodeCount\[0] = 10 * 5 = 50`.</span></span> 

## <a name="acknowledgements"></a><span data-ttu-id="efc63-373">Acknowledgements</span><span class="sxs-lookup"><span data-stu-id="efc63-373">Acknowledgements</span></span>

<span data-ttu-id="efc63-374">The Net# language for customizing the architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span><span class="sxs-lookup"><span data-stu-id="efc63-374">The Net# language for customizing the architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span></span> <span data-ttu-id="efc63-375">It is used internally for machine learning projects and applications ranging from image detection to text analytics.</span><span class="sxs-lookup"><span data-stu-id="efc63-375">It is used internally for machine learning projects and applications ranging from image detection to text analytics.</span></span> <span data-ttu-id="efc63-376">For more information, see [Neural Nets in Azure ML - Introduction to Net#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span><span class="sxs-lookup"><span data-stu-id="efc63-376">For more information, see [Neural Nets in Azure ML - Introduction to Net#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span></span>
