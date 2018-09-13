---
title: Tutorial - Distributed training with Azure Batch AI and Horovod | Microsoft Docs
description: Tutorial - How to train a distributed model with Horovod using the Azure Batch AI service and Azure CLI.
services: batch-ai
author: johnwu10
manager: jeconnoc
ms.service: batch-ai
ms.topic: tutorial
ms.date: 09/03/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: de19b20865127fd37cd7bc1ac854288a95a68091
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870858"
---
# <a name="tutorial-train-a-distributed-model-with-horovod"></a><span data-ttu-id="f8072-103">Tutorial: Train a distributed model with Horovod</span><span class="sxs-lookup"><span data-stu-id="f8072-103">Tutorial: Train a distributed model with Horovod</span></span>

<span data-ttu-id="f8072-104">In this tutorial, you train a distributed deep learning model by running it in parallel across multiple nodes in a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="f8072-104">In this tutorial, you train a distributed deep learning model by running it in parallel across multiple nodes in a Batch AI cluster.</span></span> <span data-ttu-id="f8072-105">Batch AI is a managed service for training machine learning and AI models at scale on clusters of Azure GPUs.</span><span class="sxs-lookup"><span data-stu-id="f8072-105">Batch AI is a managed service for training machine learning and AI models at scale on clusters of Azure GPUs.</span></span> 

<span data-ttu-id="f8072-106">This tutorial introduces a common Batch AI workflow along with how to interact with Batch AI resources through the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f8072-106">This tutorial introduces a common Batch AI workflow along with how to interact with Batch AI resources through the Azure CLI.</span></span> <span data-ttu-id="f8072-107">Topics covered include:</span><span class="sxs-lookup"><span data-stu-id="f8072-107">Topics covered include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8072-108">Set up a Batch AI workspace, experiment, and cluster</span><span class="sxs-lookup"><span data-stu-id="f8072-108">Set up a Batch AI workspace, experiment, and cluster</span></span>
> * <span data-ttu-id="f8072-109">Set up an Azure file share for input and output</span><span class="sxs-lookup"><span data-stu-id="f8072-109">Set up an Azure file share for input and output</span></span>
> * <span data-ttu-id="f8072-110">Parallelize a deep learning model using Horovod</span><span class="sxs-lookup"><span data-stu-id="f8072-110">Parallelize a deep learning model using Horovod</span></span>
> * <span data-ttu-id="f8072-111">Submit a training job</span><span class="sxs-lookup"><span data-stu-id="f8072-111">Submit a training job</span></span>
> * <span data-ttu-id="f8072-112">Monitor the job</span><span class="sxs-lookup"><span data-stu-id="f8072-112">Monitor the job</span></span>
> * <span data-ttu-id="f8072-113">Retrieve the training results</span><span class="sxs-lookup"><span data-stu-id="f8072-113">Retrieve the training results</span></span>

<span data-ttu-id="f8072-114">For this tutorial, an object detection model is modified to run in parallel with [Horovod](https://github.com/uber/horovod).</span><span class="sxs-lookup"><span data-stu-id="f8072-114">For this tutorial, an object detection model is modified to run in parallel with [Horovod](https://github.com/uber/horovod).</span></span> <span data-ttu-id="f8072-115">The model trains on the [CIFAR-10 dataset](https://www.cs.toronto.edu/~kriz/cifar.html) of images.</span><span class="sxs-lookup"><span data-stu-id="f8072-115">The model trains on the [CIFAR-10 dataset](https://www.cs.toronto.edu/~kriz/cifar.html) of images.</span></span> <span data-ttu-id="f8072-116">The training job runs on a cluster containing 24 vCPUs and 4 GPUs, and takes approximately 60 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f8072-116">The training job runs on a cluster containing 24 vCPUs and 4 GPUs, and takes approximately 60 minutes to complete.</span></span>

<span data-ttu-id="f8072-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f8072-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f8072-118">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="f8072-118">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="f8072-119">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f8072-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="f8072-120">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f8072-120">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span> 

## <a name="why-use-horovod"></a><span data-ttu-id="f8072-121">Why use Horovod?</span><span class="sxs-lookup"><span data-stu-id="f8072-121">Why use Horovod?</span></span>

<span data-ttu-id="f8072-122">Horovod is a distributed training framework for Tensorflow, Keras, and PyTorch, and is used for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f8072-122">Horovod is a distributed training framework for Tensorflow, Keras, and PyTorch, and is used for this tutorial.</span></span> <span data-ttu-id="f8072-123">With Horovod, you can convert a training script designed to run on a single GPU to one that runs efficiently on a distributed system using just a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="f8072-123">With Horovod, you can convert a training script designed to run on a single GPU to one that runs efficiently on a distributed system using just a few lines of code.</span></span>

<span data-ttu-id="f8072-124">In addition to Horovod, Batch AI supports distributed training with several other popular open-source frameworks.</span><span class="sxs-lookup"><span data-stu-id="f8072-124">In addition to Horovod, Batch AI supports distributed training with several other popular open-source frameworks.</span></span> <span data-ttu-id="f8072-125">Be sure to review the license terms of any framework that you use to train models in production.</span><span class="sxs-lookup"><span data-stu-id="f8072-125">Be sure to review the license terms of any framework that you use to train models in production.</span></span>

## <a name="prepare-the-batch-ai-environment"></a><span data-ttu-id="f8072-126">Prepare the Batch AI environment</span><span class="sxs-lookup"><span data-stu-id="f8072-126">Prepare the Batch AI environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f8072-127">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f8072-127">Create a resource group</span></span>

<span data-ttu-id="f8072-128">Use the `az group create` command to create a resource group named `batchai.horovod` in the `eastus` region.</span><span class="sxs-lookup"><span data-stu-id="f8072-128">Use the `az group create` command to create a resource group named `batchai.horovod` in the `eastus` region.</span></span> <span data-ttu-id="f8072-129">You use the resource group to deploy Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="f8072-129">You use the resource group to deploy Batch AI resources.</span></span>

```azurecli-interactive
az group create --name batchai.horovod --location eastus
```

### <a name="create-a-workspace"></a><span data-ttu-id="f8072-130">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="f8072-130">Create a workspace</span></span>

<span data-ttu-id="f8072-131">Create a Batch AI workspace using the `az batchai workspace create` command.</span><span class="sxs-lookup"><span data-stu-id="f8072-131">Create a Batch AI workspace using the `az batchai workspace create` command.</span></span> <span data-ttu-id="f8072-132">A workspace is a top-level collection of other Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="f8072-132">A workspace is a top-level collection of other Batch AI resources.</span></span> <span data-ttu-id="f8072-133">The following command creates a workspace called `batchaidev` under your resource group.</span><span class="sxs-lookup"><span data-stu-id="f8072-133">The following command creates a workspace called `batchaidev` under your resource group.</span></span>

```azurecli-interactive
az batchai workspace create --resource-group batchai.horovod --workspace batchaidev 
```

### <a name="create-an-experiment"></a><span data-ttu-id="f8072-134">Create an experiment</span><span class="sxs-lookup"><span data-stu-id="f8072-134">Create an experiment</span></span>

<span data-ttu-id="f8072-135">A Batch AI experiment groups one or more jobs that you query and manage together.</span><span class="sxs-lookup"><span data-stu-id="f8072-135">A Batch AI experiment groups one or more jobs that you query and manage together.</span></span> <span data-ttu-id="f8072-136">The following `az batchai experiment create` command creates an experiment called `cifar` under the workspace and resource group.</span><span class="sxs-lookup"><span data-stu-id="f8072-136">The following `az batchai experiment create` command creates an experiment called `cifar` under the workspace and resource group.</span></span>

```azurecli-interactive
az batchai experiment create --resource-group batchai.horovod --workspace batchaidev --name cifar 
```

## <a name="set-up-a-gpu-cluster"></a><span data-ttu-id="f8072-137">Set up a GPU cluster</span><span class="sxs-lookup"><span data-stu-id="f8072-137">Set up a GPU cluster</span></span>

<span data-ttu-id="f8072-138">Next, set up a GPU cluster to run the experiment.</span><span class="sxs-lookup"><span data-stu-id="f8072-138">Next, set up a GPU cluster to run the experiment.</span></span> <span data-ttu-id="f8072-139">Batch AI provides a flexible range of options for customizing clusters for specific needs.</span><span class="sxs-lookup"><span data-stu-id="f8072-139">Batch AI provides a flexible range of options for customizing clusters for specific needs.</span></span>

<span data-ttu-id="f8072-140">The following `az batchai cluster create` command creates a 4-node cluster called `nc6cluster` under your workspace and resource group.</span><span class="sxs-lookup"><span data-stu-id="f8072-140">The following `az batchai cluster create` command creates a 4-node cluster called `nc6cluster` under your workspace and resource group.</span></span> <span data-ttu-id="f8072-141">By default, the VMs in the cluster run an Ubuntu Server image designed to host container-based applications.</span><span class="sxs-lookup"><span data-stu-id="f8072-141">By default, the VMs in the cluster run an Ubuntu Server image designed to host container-based applications.</span></span> <span data-ttu-id="f8072-142">The cluster nodes in this example use the `Standard_NC6` size, which contains one NVIDIA Tesla K80 GPU.</span><span class="sxs-lookup"><span data-stu-id="f8072-142">The cluster nodes in this example use the `Standard_NC6` size, which contains one NVIDIA Tesla K80 GPU.</span></span>

```azurecli-interactive
az batchai cluster create --resource-group batchai.horovod --workspace batchaidev --name nc6cluster --vm-priority dedicated  --vm-size Standard_NC6 --target 4 --generate-ssh-keys
```

<span data-ttu-id="f8072-143">Run the `az batchai cluster show` command to view the cluster status.</span><span class="sxs-lookup"><span data-stu-id="f8072-143">Run the `az batchai cluster show` command to view the cluster status.</span></span> <span data-ttu-id="f8072-144">It usually takes a few minutes to fully provision the cluster.</span><span class="sxs-lookup"><span data-stu-id="f8072-144">It usually takes a few minutes to fully provision the cluster.</span></span>

```azurecli-interactive
az batchai cluster show --name nc6cluster --workspace batchaidev --resource-group batchai.horovod --output table
```

<span data-ttu-id="f8072-145">Early in cluster creation, the cluster is in the `resizing` state.</span><span class="sxs-lookup"><span data-stu-id="f8072-145">Early in cluster creation, the cluster is in the `resizing` state.</span></span> <span data-ttu-id="f8072-146">Continue the following steps while the cluster state changes.</span><span class="sxs-lookup"><span data-stu-id="f8072-146">Continue the following steps while the cluster state changes.</span></span> <span data-ttu-id="f8072-147">The cluster is ready to run the training job when the state is `steady`and the nodes are `idle`.</span><span class="sxs-lookup"><span data-stu-id="f8072-147">The cluster is ready to run the training job when the state is `steady`and the nodes are `idle`.</span></span> <span data-ttu-id="f8072-148">For example:</span><span class="sxs-lookup"><span data-stu-id="f8072-148">For example:</span></span>

```
Name        Resource Group    Workspace    VM Size       State      Idle    Running    Preparing    Leaving    Unusable
----------  ----------------  -----------  ------------  -------  ------  ---------  -----------  ---------  ----------
nc6cluster  batchai.horovod  batchaidev   STANDARD_NC6  steady        4          0            0          0           0
```

## <a name="set-up-storage"></a><span data-ttu-id="f8072-149">Set up storage</span><span class="sxs-lookup"><span data-stu-id="f8072-149">Set up storage</span></span>

<span data-ttu-id="f8072-150">Use the `az storage account create` command to create a storage account to store your training script and training output.</span><span class="sxs-lookup"><span data-stu-id="f8072-150">Use the `az storage account create` command to create a storage account to store your training script and training output.</span></span>

```azurecli-interactive
az storage account create --resource-group batchai.horovod --name mystorageaccount --location eastus --sku Standard_LRS
```

<span data-ttu-id="f8072-151">Create an Azure file share called `myshare` in the account, using the `az storage share create` command:</span><span class="sxs-lookup"><span data-stu-id="f8072-151">Create an Azure file share called `myshare` in the account, using the `az storage share create` command:</span></span>

```azurecli-interactive
az storage share create --name myshare --account-name mystorageaccount
```

<span data-ttu-id="f8072-152">In practice, this same storage can be used across multiple jobs and experiments.</span><span class="sxs-lookup"><span data-stu-id="f8072-152">In practice, this same storage can be used across multiple jobs and experiments.</span></span> <span data-ttu-id="f8072-153">To keep things organized, create a directory within the file share to store files related to this specific experiment.</span><span class="sxs-lookup"><span data-stu-id="f8072-153">To keep things organized, create a directory within the file share to store files related to this specific experiment.</span></span> <span data-ttu-id="f8072-154">The following `az storage directory create` command creates a directory called `cifar`.</span><span class="sxs-lookup"><span data-stu-id="f8072-154">The following `az storage directory create` command creates a directory called `cifar`.</span></span>

```azurecli-interactive
az storage directory create --name cifar --share-name myshare --account-name mystorageaccount
```

<span data-ttu-id="f8072-155">The next step is to prepare the actual training script, which you then upload to the newly created directory.</span><span class="sxs-lookup"><span data-stu-id="f8072-155">The next step is to prepare the actual training script, which you then upload to the newly created directory.</span></span>

## <a name="create-the-training-script"></a><span data-ttu-id="f8072-156">Create the training script</span><span class="sxs-lookup"><span data-stu-id="f8072-156">Create the training script</span></span>

<span data-ttu-id="f8072-157">For this experiment, you run a Python script that is updated with a few  changes in order to run an object detection model in parallel using Horovod.</span><span class="sxs-lookup"><span data-stu-id="f8072-157">For this experiment, you run a Python script that is updated with a few  changes in order to run an object detection model in parallel using Horovod.</span></span> <span data-ttu-id="f8072-158">The [original model](https://raw.githubusercontent.com/keras-team/keras/master/examples/cifar10_cnn.py) uses Keras with a TensorFlow backend.</span><span class="sxs-lookup"><span data-stu-id="f8072-158">The [original model](https://raw.githubusercontent.com/keras-team/keras/master/examples/cifar10_cnn.py) uses Keras with a TensorFlow backend.</span></span> 

<span data-ttu-id="f8072-159">In a working directory in your shell, use your favorite text editor to create a file named `cifar_cnn_distributed.py` with the following content.</span><span class="sxs-lookup"><span data-stu-id="f8072-159">In a working directory in your shell, use your favorite text editor to create a file named `cifar_cnn_distributed.py` with the following content.</span></span> <span data-ttu-id="f8072-160">Changes to the original source code are commented with a `HOROVOD` prefix.</span><span class="sxs-lookup"><span data-stu-id="f8072-160">Changes to the original source code are commented with a `HOROVOD` prefix.</span></span>

```python
from __future__ import print_function
import keras
from keras.datasets import cifar10
from keras.preprocessing.image import ImageDataGenerator
from keras.models import Sequential
from keras.layers import Dense, Dropout, Activation, Flatten
from keras.layers import Conv2D, MaxPooling2D
import tensorflow as tf
import horovod.keras as hvd
import os
from keras import backend as K
import math
import argparse 

# HOROVOD: initialize Horovod.
hvd.init()

# HOROVOD: pin GPU to be used to process local rank (one GPU per process)
config = tf.ConfigProto()
config.gpu_options.allow_growth = True
config.gpu_options.visible_device_list = str(hvd.local_rank())
K.set_session(tf.Session(config=config))

batch_size = 32
num_classes = 10
# HOROVOD: adjust number of epochs based on number of GPUs.
epochs = int(math.ceil(100.0 / hvd.size()))

data_augmentation = True
num_predictions = 20
# BATCH AI: change save directory to mounted storage path
parser = argparse.ArgumentParser()
parser.add_argument("-d", "--dir", help="directory to save model to")
args = parser.parse_args()
save_dir = os.path.join(args.dir, 'saved_models')
model_name = 'keras_cifar10_trained_model.h5'

# The data, split between train and test sets:
(x_train, y_train), (x_test, y_test) = cifar10.load_data()
print('x_train shape:', x_train.shape)
print(x_train.shape[0], 'train samples')
print(x_test.shape[0], 'test samples')

# Convert class vectors to binary class matrices.
y_train = keras.utils.to_categorical(y_train, num_classes)
y_test = keras.utils.to_categorical(y_test, num_classes)

model = Sequential()
model.add(Conv2D(32, (3, 3), padding='same',
                 input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(32, (3, 3)))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))

model.add(Conv2D(64, (3, 3), padding='same'))
model.add(Activation('relu'))
model.add(Conv2D(64, (3, 3)))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))

model.add(Flatten())
model.add(Dense(512))
model.add(Activation('relu'))
model.add(Dropout(0.5))
model.add(Dense(num_classes))
model.add(Activation('softmax'))

# HOROVOD: adjust learning rate based on number of GPUs.
opt = keras.optimizers.rmsprop(lr=0.0001 * hvd.size(), decay=1e-6)

# HOROVOD: add Horovod Distributed Optimizer.
opt = hvd.DistributedOptimizer(opt)

# Let's train the model using RMSprop
model.compile(loss='categorical_crossentropy',
              optimizer=opt,
              metrics=['accuracy'])

callbacks = [
    # HOROVOD: broadcast initial variable states from rank 0 to all other processes.
    # This is necessary to ensure consistent initialization of all workers when
    # training is started with random weights or restored from a checkpoint.
    hvd.callbacks.BroadcastGlobalVariablesCallback(0),
]

# HOROVOD: save checkpoints only on worker 0 to prevent other workers from corrupting them.
if hvd.rank() == 0:
    callbacks.append(keras.callbacks.ModelCheckpoint('./checkpoint-{epoch}.h5'))

x_train = x_train.astype('float32')
x_test = x_test.astype('float32')
x_train /= 255
x_test /= 255

if not data_augmentation:
    print('Not using data augmentation.')
    model.fit(x_train, y_train,
              batch_size=batch_size,
              epochs=epochs,
              validation_data=(x_test, y_test),
              shuffle=True)
else:
    print('Using real-time data augmentation.')
    # This will do preprocessing and realtime data augmentation:
    datagen = ImageDataGenerator(
        featurewise_center=False,  # set input mean to 0 over the dataset
        samplewise_center=False,  # set each sample mean to 0
        featurewise_std_normalization=False,  # divide inputs by std of the dataset
        samplewise_std_normalization=False,  # divide each input by its std
        zca_whitening=False,  # apply ZCA whitening
        zca_epsilon=1e-06,  # epsilon for ZCA whitening
        rotation_range=0,  # randomly rotate images in the range (degrees, 0 to 180)
        width_shift_range=0.1,  # randomly shift images horizontally (fraction of total width)
        height_shift_range=0.1,  # randomly shift images vertically (fraction of total height)
        shear_range=0.,  # set range for random shear
        zoom_range=0.,  # set range for random zoom
        channel_shift_range=0.,  # set range for random channel shifts
        fill_mode='nearest',  # set mode for filling points outside the input boundaries
        cval=0.,  # value used for fill_mode = "constant"
        horizontal_flip=True,  # randomly flip images
        vertical_flip=False,  # randomly flip images
        rescale=None,  # set rescaling factor (applied before any other transformation)
        preprocessing_function=None,  # set function that will be applied on each input
        data_format=None,  # image data format, either "channels_first" or "channels_last"
        validation_split=0.0)  # fraction of images reserved for validation (strictly between 0 and 1)

    # Compute quantities required for feature-wise normalization
    # (std, mean, and principal components if ZCA whitening is applied).
    datagen.fit(x_train)

    # Fit the model on the batches generated by datagen.flow().
    model.fit_generator(datagen.flow(x_train, y_train,
                                     batch_size=batch_size),
                        epochs=epochs,
                        validation_data=(x_test, y_test),
                        workers=4)

# Save model and weights
if not os.path.isdir(save_dir):
    os.makedirs(save_dir)
model_path = os.path.join(save_dir, model_name)
model.save(model_path)
print('Saved trained model at %s ' % model_path)

# Score trained model.
scores = model.evaluate(x_test, y_test, verbose=1)
print('Test loss:', scores[0])
print('Test accuracy:', scores[1])
```

<span data-ttu-id="f8072-161">As shown in this example, only a few updates to the model are needed to enable distributed training using the Horovod framework.</span><span class="sxs-lookup"><span data-stu-id="f8072-161">As shown in this example, only a few updates to the model are needed to enable distributed training using the Horovod framework.</span></span> 

<span data-ttu-id="f8072-162">Keep in mind that this script uses a relatively small model and dataset for demo purposes, so this distributed model will not necessarily show a substantial performance improvement.</span><span class="sxs-lookup"><span data-stu-id="f8072-162">Keep in mind that this script uses a relatively small model and dataset for demo purposes, so this distributed model will not necessarily show a substantial performance improvement.</span></span> <span data-ttu-id="f8072-163">To truly see the power of distributed training, use a much larger model and dataset.</span><span class="sxs-lookup"><span data-stu-id="f8072-163">To truly see the power of distributed training, use a much larger model and dataset.</span></span>

## <a name="upload-the-training-script"></a><span data-ttu-id="f8072-164">Upload the training script</span><span class="sxs-lookup"><span data-stu-id="f8072-164">Upload the training script</span></span>

<span data-ttu-id="f8072-165">Once the script is ready, the next step is to upload it to the file share directory that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f8072-165">Once the script is ready, the next step is to upload it to the file share directory that you created earlier.</span></span> <span data-ttu-id="f8072-166">The following `az storage file upload` command uploads it from the local working directory to the proper location.</span><span class="sxs-lookup"><span data-stu-id="f8072-166">The following `az storage file upload` command uploads it from the local working directory to the proper location.</span></span>

```azurecli-interactive
az storage file upload --path cifar --share-name myshare --source cifar_cnn_distributed.py --account-name mystorageaccount
```

## <a name="submit-the-training-job"></a><span data-ttu-id="f8072-167">Submit the training job</span><span class="sxs-lookup"><span data-stu-id="f8072-167">Submit the training job</span></span>

<span data-ttu-id="f8072-168">After completing the previous steps, create a training job.</span><span class="sxs-lookup"><span data-stu-id="f8072-168">After completing the previous steps, create a training job.</span></span> <span data-ttu-id="f8072-169">In Batch AI, you use a `job.json` file to define the parameters for how to run a job.</span><span class="sxs-lookup"><span data-stu-id="f8072-169">In Batch AI, you use a `job.json` file to define the parameters for how to run a job.</span></span> <span data-ttu-id="f8072-170">Using your favorite text editor, create a job configuration file called `job.json` with the following content.</span><span class="sxs-lookup"><span data-stu-id="f8072-170">Using your favorite text editor, create a job configuration file called `job.json` with the following content.</span></span>

```json
{
    "$schema": "https://raw.githubusercontent.com/Azure/BatchAI/master/schemas/2018-05-01/job.json",
    "properties": {
        "nodeCount": 4,
        "horovodSettings": {
            "pythonScriptFilePath": "$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare/cifar/cifar_cnn_distributed.py",
            "commandLineArgs": "--dir=$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare/cifar"
        },
        "stdOutErrPathPrefix": "$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare/cifar",
        "mountVolumes": {
            "azureFileShares": [
                {
                    "azureFileUrl": "https://<AZURE_BATCHAI_STORAGE_ACCOUNT>.file.core.windows.net/myshare",
                    "relativeMountPath": "myshare"
                }
            ]
        },
        "jobPreparation": {
            "commandLine": "apt update; apt install mpi-default-dev mpi-default-bin -y; pip install keras horovod"
        },
        "containerSettings": {
            "imageSourceRegistry": {
                "image": "tensorflow/tensorflow:1.8.0-gpu"
            }
        }
    }
}
```

<span data-ttu-id="f8072-171">Explanation of properties:</span><span class="sxs-lookup"><span data-stu-id="f8072-171">Explanation of properties:</span></span>

| <span data-ttu-id="f8072-172">Property</span><span class="sxs-lookup"><span data-stu-id="f8072-172">Property</span></span> | <span data-ttu-id="f8072-173">Description</span><span class="sxs-lookup"><span data-stu-id="f8072-173">Description</span></span> |
| --------- | --------- |
| `nodeCount` | <span data-ttu-id="f8072-174">The number of nodes to dedicate for the job.</span><span class="sxs-lookup"><span data-stu-id="f8072-174">The number of nodes to dedicate for the job.</span></span> <span data-ttu-id="f8072-175">Here, the job will run in parallel on `4` nodes.</span><span class="sxs-lookup"><span data-stu-id="f8072-175">Here, the job will run in parallel on `4` nodes.</span></span> |
| `horovodSettings` | <span data-ttu-id="f8072-176">The `pythonScriptFilePath` field defines the path to the Horovod script, located in the `cifar` directory created previously.</span><span class="sxs-lookup"><span data-stu-id="f8072-176">The `pythonScriptFilePath` field defines the path to the Horovod script, located in the `cifar` directory created previously.</span></span> <span data-ttu-id="f8072-177">The `commandLineArgs` field is the command-line arguments for running the script.</span><span class="sxs-lookup"><span data-stu-id="f8072-177">The `commandLineArgs` field is the command-line arguments for running the script.</span></span> <span data-ttu-id="f8072-178">For this experiment, the directory of where to save the model is the only required argument.</span><span class="sxs-lookup"><span data-stu-id="f8072-178">For this experiment, the directory of where to save the model is the only required argument.</span></span> <span data-ttu-id="f8072-179">`$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare` is the path where the file share was mounted.</span><span class="sxs-lookup"><span data-stu-id="f8072-179">`$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare` is the path where the file share was mounted.</span></span> | 
| `stdOutErrPathPrefix` | <span data-ttu-id="f8072-180">The path to store the job outputs and logs, which for this example is the same `cifar` directory.</span><span class="sxs-lookup"><span data-stu-id="f8072-180">The path to store the job outputs and logs, which for this example is the same `cifar` directory.</span></span> |
| `jobPreparation` | <span data-ttu-id="f8072-181">Any special instructions for preparing the environment for running the job.</span><span class="sxs-lookup"><span data-stu-id="f8072-181">Any special instructions for preparing the environment for running the job.</span></span> <span data-ttu-id="f8072-182">This script requires installation of the indicated MPI and Horovod packages.</span><span class="sxs-lookup"><span data-stu-id="f8072-182">This script requires installation of the indicated MPI and Horovod packages.</span></span> |
| `containerSettings` | <span data-ttu-id="f8072-183">Settings for the container that the job runs on.</span><span class="sxs-lookup"><span data-stu-id="f8072-183">Settings for the container that the job runs on.</span></span> <span data-ttu-id="f8072-184">This job uses a Docker container built with `tensorflow`.</span><span class="sxs-lookup"><span data-stu-id="f8072-184">This job uses a Docker container built with `tensorflow`.</span></span>

<span data-ttu-id="f8072-185">Using the configuration, create the job using the `az batchai job create` command.</span><span class="sxs-lookup"><span data-stu-id="f8072-185">Using the configuration, create the job using the `az batchai job create` command.</span></span> <span data-ttu-id="f8072-186">The following command queues a new job called `cifar_distributed` using all the resources that have been set up to this point.</span><span class="sxs-lookup"><span data-stu-id="f8072-186">The following command queues a new job called `cifar_distributed` using all the resources that have been set up to this point.</span></span> 

```azurecli-interactive
az batchai job create --cluster nc6cluster --name cifar_distributed --resource-group batchai.horovod --workspace batchaidev --experiment cifar --config-file job.json --storage-account-name mystorageaccount
```

<span data-ttu-id="f8072-187">If the nodes are currently busy, the job may take a while before to start running.</span><span class="sxs-lookup"><span data-stu-id="f8072-187">If the nodes are currently busy, the job may take a while before to start running.</span></span> <span data-ttu-id="f8072-188">Use the `az batchai job show` command to view the execution state of the job.</span><span class="sxs-lookup"><span data-stu-id="f8072-188">Use the `az batchai job show` command to view the execution state of the job.</span></span>

```azurecli-interactive
az batchai job show --experiment cifar --name cifar_distributed --resource-group batchai.horovod --workspace batchaidev --query "executionState"
```

### <a name="visualize-the-distributed-training"></a><span data-ttu-id="f8072-189">Visualize the distributed training</span><span class="sxs-lookup"><span data-stu-id="f8072-189">Visualize the distributed training</span></span>

<span data-ttu-id="f8072-190">Once the job starts running, use the `az batchai cluster show` command again to query the status of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="f8072-190">Once the job starts running, use the `az batchai cluster show` command again to query the status of the cluster nodes.</span></span> 

```azurecli-interactive
az batchai cluster show --name nc6cluster --workspace batchaidev --resource-group batchai.horovod --query "nodeStateCounts"
```

<span data-ttu-id="f8072-191">The output should be similar to the following, which shows all four in a running state.</span><span class="sxs-lookup"><span data-stu-id="f8072-191">The output should be similar to the following, which shows all four in a running state.</span></span> <span data-ttu-id="f8072-192">This result shows that all four nodes are currently being utilized in the distributed training.</span><span class="sxs-lookup"><span data-stu-id="f8072-192">This result shows that all four nodes are currently being utilized in the distributed training.</span></span>

```
{
  "idleNodeCount": 0,
  "leavingNodeCount": 0,
  "preparingNodeCount": 0,
  "runningNodeCount": 4,
  "unusableNodeCount": 0
}
```

## <a name="monitor-the-job"></a><span data-ttu-id="f8072-193">Monitor the job</span><span class="sxs-lookup"><span data-stu-id="f8072-193">Monitor the job</span></span>

### <a name="list-output-files"></a><span data-ttu-id="f8072-194">List output files</span><span class="sxs-lookup"><span data-stu-id="f8072-194">List output files</span></span>

<span data-ttu-id="f8072-195">While the job is running, use the `az batchai job file list` command to list the output files that the job generates.</span><span class="sxs-lookup"><span data-stu-id="f8072-195">While the job is running, use the `az batchai job file list` command to list the output files that the job generates.</span></span>

```azurecli-interactive
az batchai job file list --experiment cifar --job cifar_distributed --resource-group batchai.horovod --workspace batchaidev --output table
```

<span data-ttu-id="f8072-196">For this specific experiment, the output should be similar to the following.</span><span class="sxs-lookup"><span data-stu-id="f8072-196">For this specific experiment, the output should be similar to the following.</span></span> <span data-ttu-id="f8072-197">The overall output for the job is logged to `stdout.txt` while `stderr.txt` outputs any errors that occur in the main execution.</span><span class="sxs-lookup"><span data-stu-id="f8072-197">The overall output for the job is logged to `stdout.txt` while `stderr.txt` outputs any errors that occur in the main execution.</span></span> <span data-ttu-id="f8072-198">The other files are output, error, and job preparation logs corresponding to each individual node.</span><span class="sxs-lookup"><span data-stu-id="f8072-198">The other files are output, error, and job preparation logs corresponding to each individual node.</span></span>

```
Name                                                    Type       Size  Modified
------------------------------------------------------  ------  -------  -------------------------
execution-tvm-676767296_1-20180718t174802z-p.log        file       8801  2018-07-18T22:41:28+00:00
execution-tvm-676767296_2-20180718t174802z-p.log        file      15094  2018-07-18T22:41:55+00:00
execution-tvm-676767296_3-20180718t174802z-p.log        file       8801  2018-07-18T22:41:28+00:00
execution-tvm-676767296_4-20180718t174802z-p.log        file       8801  2018-07-18T22:41:28+00:00
stderr-job_prep-tvm-676767296_1-20180718t174802z-p.txt  file        238  2018-07-18T22:41:50+00:00
stderr-job_prep-tvm-676767296_2-20180718t174802z-p.txt  file        238  2018-07-18T22:41:50+00:00
stderr-job_prep-tvm-676767296_3-20180718t174802z-p.txt  file        238  2018-07-18T22:41:50+00:00
stderr-job_prep-tvm-676767296_4-20180718t174802z-p.txt  file        238  2018-07-18T22:41:50+00:00
stderr.txt                                              file       7653  2018-07-18T22:46:32+00:00
stdout-job_prep-tvm-676767296_1-20180718t174802z-p.txt  file      13651  2018-07-18T22:41:55+00:00
stdout-job_prep-tvm-676767296_2-20180718t174802z-p.txt  file      13651  2018-07-18T22:41:54+00:00
stdout-job_prep-tvm-676767296_3-20180718t174802z-p.txt  file      13651  2018-07-18T22:41:54+00:00
stdout-job_prep-tvm-676767296_4-20180718t174802z-p.txt  file      13651  2018-07-18T22:41:55+00:00
stdout.txt                                              file    2316480  2018-07-18T22:46:32+00:00
```

### <a name="stream-an-output-file"></a><span data-ttu-id="f8072-199">Stream an output file</span><span class="sxs-lookup"><span data-stu-id="f8072-199">Stream an output file</span></span>

<span data-ttu-id="f8072-200">Use the `az batchai job file stream` command to stream the contents of a file.</span><span class="sxs-lookup"><span data-stu-id="f8072-200">Use the `az batchai job file stream` command to stream the contents of a file.</span></span> <span data-ttu-id="f8072-201">The following example streams the main output log.</span><span class="sxs-lookup"><span data-stu-id="f8072-201">The following example streams the main output log.</span></span>

```azurecli-interactive
az batchai job file stream --experiment cifar --file-name stdout.txt --job cifar_distributed --resource-group batchai.horovod --workspace batchaidev
```

<span data-ttu-id="f8072-202">While the job runs, the command streams the standard output of the training job, showing output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="f8072-202">While the job runs, the command streams the standard output of the training job, showing output similar to the following.</span></span>

```
...
50000 train samples
10000 test samples
Using real-time data augmentation.
Epoch 1/25


   1/1563 [..............................] - ETA: 2:42:25 - loss: 2.3334 - acc: 0.0312   1/1563 [..............................] - ETA: 2:30:42 - loss: 2.2973 - acc: 0.0938
   1/1563 [..............................] - ETA: 30:36 - loss: 2.3175 - acc: 0.1250
   1/1563 [..............................] - ETA: 2:32:58 - loss: 2.3489 - acc: 0.0625
   2/1563 [..............................] - ETA: 1:21:59 - loss: 2.3230 - acc: 0.0625

   2/1563 [..............................]   2/1563 [..............................] - ETA: 1:16:09 - loss: 2.2913 - acc: 0.0938 - ETA: 1:17:15 - loss: 2.3147 - acc: 0.0781
   2/1563 [..............................] - ETA: 16:07 - loss: 2.3678 - acc: 0.0938
   3/1563 [..............................] - ETA: 55:05 - loss: 2.3232 - acc: 0.0938  
   3/1563 [..............................] - ETA: 51:57 - loss: 2.3185 - acc: 0.1146  
   3/1563 [..............................] - ETA: 51:12 - loss: 2.3179 - acc: 0.1042  
   3/1563 [..............................] - ETA: 11:13 - loss: 2.3504 - acc: 0.0833
   4/1563 [..............................] - ETA: 39:43 - loss: 2.3224 - acc: 0.1094
   4/1563 [..............................] - ETA: 42:09 - loss: 2.3049 - acc: 0.1250
   4/1563 [..............................] - ETA: 39:15 - loss: 2.3089 - acc: 0.1094
   4/1563 [..............................] - ETA: 9:16 - loss: 2.3316 - acc: 0.1016 
   5/1563 [..............................] - ETA: 39:51 - loss: 2.3153 - acc: 0.1125
   5/1563 [..............................] - ETA: 37:58 - loss: 2.3197 - acc: 0.1125
   5/1563 [..............................] - ETA: 37:35 - loss: 2.3148 - acc: 0.1062
   5/1563 [..............................] - ETA: 13:38 - loss: 2.3263 - acc: 0.1062
   6/1563 [..............................] - ETA: 35:48 - loss: 2.3168 - acc: 0.1198

   6/1563 [..............................]   6/1563 [..............................] - ETA: 34:13 - loss: 2.3142 - acc: 0.1198 - ETA: 33:51 - loss: 2.3162 - acc: 0.1042
   6/1563 [..............................] - ETA: 13:54 - loss: 2.3225 - acc: 0.1094
   7/1563 [..............................] - ETA: 30:53 - loss: 2.3181 - acc: 0.1071

   7/1563 [..............................]   7/1563 [..............................] - ETA: 29:32 - loss: 2.3149 - acc: 0.1161 - ETA: 29:13 - loss: 2.3140 - acc: 0.0938
   7/1563 [..............................] - ETA: 12:09 - loss: 2.3174 - acc: 0.1205
   8/1563 [..............................] - ETA: 26:04 - loss: 2.3113 - acc: 0.1133
   8/1563 [..............................] - ETA: 27:15 - loss: 2.3169 - acc: 0.1133
   8/1563 [..............................] - ETA: 10:51 - loss: 2.3152 - acc: 0.1172
...
```

<span data-ttu-id="f8072-203">The script trains over 25 epochs, or passes through the training dataset.</span><span class="sxs-lookup"><span data-stu-id="f8072-203">The script trains over 25 epochs, or passes through the training dataset.</span></span> <span data-ttu-id="f8072-204">This process takes approximately 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="f8072-204">This process takes approximately 60 minutes.</span></span> 

## <a name="retrieve-the-results"></a><span data-ttu-id="f8072-205">Retrieve the results</span><span class="sxs-lookup"><span data-stu-id="f8072-205">Retrieve the results</span></span>

<span data-ttu-id="f8072-206">When the script completes, if everything went well, the validation accuracy should be about 70-75% and the trained model is saved to the file share at `cifar/saved_models/keras_cifar10_trained_model.h5`.</span><span class="sxs-lookup"><span data-stu-id="f8072-206">When the script completes, if everything went well, the validation accuracy should be about 70-75% and the trained model is saved to the file share at `cifar/saved_models/keras_cifar10_trained_model.h5`.</span></span> 

<span data-ttu-id="f8072-207">Model training is usually a part of a larger workflow.</span><span class="sxs-lookup"><span data-stu-id="f8072-207">Model training is usually a part of a larger workflow.</span></span> <span data-ttu-id="f8072-208">For example, you might expose the trained model in another application.</span><span class="sxs-lookup"><span data-stu-id="f8072-208">For example, you might expose the trained model in another application.</span></span> <span data-ttu-id="f8072-209">To download the trained model locally, use the `az storage file download` command.</span><span class="sxs-lookup"><span data-stu-id="f8072-209">To download the trained model locally, use the `az storage file download` command.</span></span> 

```azurecli-interactive
az storage file download --path cifar/saved_models/keras_cifar10_trained_model.h5 --share-name myshare --account-name mystorageaccount
```
## <a name="clean-up-resources"></a><span data-ttu-id="f8072-210">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f8072-210">Clean up resources</span></span>

<span data-ttu-id="f8072-211">Once jobs are finished running, a best practice for saving compute costs is to downscale all clusters to `0 nodes` so that you don't get charged for idle time.</span><span class="sxs-lookup"><span data-stu-id="f8072-211">Once jobs are finished running, a best practice for saving compute costs is to downscale all clusters to `0 nodes` so that you don't get charged for idle time.</span></span> <span data-ttu-id="f8072-212">Use the following `az batchai cluster resize` command.</span><span class="sxs-lookup"><span data-stu-id="f8072-212">Use the following `az batchai cluster resize` command.</span></span> 

```azurecli-interactive
az batchai cluster resize --name nc6cluster --resource-group batchai.horovod --target 0 --workspace batchaidev
```

<span data-ttu-id="f8072-213">Later, resize it to 1 or more nodes to run your jobs.</span><span class="sxs-lookup"><span data-stu-id="f8072-213">Later, resize it to 1 or more nodes to run your jobs.</span></span> 

<span data-ttu-id="f8072-214">If you don't plan to use the workspace and storage account in the future, delete the resource group using the `az group delete` command.</span><span class="sxs-lookup"><span data-stu-id="f8072-214">If you don't plan to use the workspace and storage account in the future, delete the resource group using the `az group delete` command.</span></span> <span data-ttu-id="f8072-215">Deleting a resource group deletes all resources that are part of that group.</span><span class="sxs-lookup"><span data-stu-id="f8072-215">Deleting a resource group deletes all resources that are part of that group.</span></span>

```azurecli-interactive
az group delete --name batchai.horovod
```

## <a name="next-steps"></a><span data-ttu-id="f8072-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8072-216">Next steps</span></span>

<span data-ttu-id="f8072-217">In this tutorial, you learned about how to:</span><span class="sxs-lookup"><span data-stu-id="f8072-217">In this tutorial, you learned about how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8072-218">Set up a Batch AI workspace, experiment, and cluster</span><span class="sxs-lookup"><span data-stu-id="f8072-218">Set up a Batch AI workspace, experiment, and cluster</span></span>
> * <span data-ttu-id="f8072-219">Set up an Azure file share for input and output</span><span class="sxs-lookup"><span data-stu-id="f8072-219">Set up an Azure file share for input and output</span></span>
> * <span data-ttu-id="f8072-220">Parallelize a model using Horovod</span><span class="sxs-lookup"><span data-stu-id="f8072-220">Parallelize a model using Horovod</span></span>
> * <span data-ttu-id="f8072-221">Submit a training job</span><span class="sxs-lookup"><span data-stu-id="f8072-221">Submit a training job</span></span>
> * <span data-ttu-id="f8072-222">Monitor the job</span><span class="sxs-lookup"><span data-stu-id="f8072-222">Monitor the job</span></span>
> * <span data-ttu-id="f8072-223">Retrieve the training results</span><span class="sxs-lookup"><span data-stu-id="f8072-223">Retrieve the training results</span></span>

<span data-ttu-id="f8072-224">For examples of using Batch AI with different frameworks, see the recipes on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8072-224">For examples of using Batch AI with different frameworks, see the recipes on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8072-225">Batch AI recipes</span><span class="sxs-lookup"><span data-stu-id="f8072-225">Batch AI recipes</span></span>](https://github.com/Azure/BatchAI/tree/master/recipes)
