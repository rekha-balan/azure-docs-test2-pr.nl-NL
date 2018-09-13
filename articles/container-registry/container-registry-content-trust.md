---
title: Content trust in Azure Container Registry
description: Learn how enable content trust for your Azure container registry, and push and pull signed images.
services: container-registry
author: mmacy
ms.service: container-registry
ms.topic: quickstart
ms.date: 08/20/2018
ms.author: marsma
ms.openlocfilehash: 5dd8bc4227fda4c5d4def4b59bd7ff9a707f47f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967224"
---
# <a name="content-trust-in-azure-container-registry"></a><span data-ttu-id="fa402-103">Content trust in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="fa402-103">Content trust in Azure Container Registry</span></span>

<span data-ttu-id="fa402-104">Important to any distributed system designed with security in mind is verifying both the *source* and the *integrity* of data entering the system.</span><span class="sxs-lookup"><span data-stu-id="fa402-104">Important to any distributed system designed with security in mind is verifying both the *source* and the *integrity* of data entering the system.</span></span> <span data-ttu-id="fa402-105">Consumers of the data need to be able to verify both the publisher (source) of the data, as well as ensure it's not been modified after it was published (integrity).</span><span class="sxs-lookup"><span data-stu-id="fa402-105">Consumers of the data need to be able to verify both the publisher (source) of the data, as well as ensure it's not been modified after it was published (integrity).</span></span> <span data-ttu-id="fa402-106">Azure Container Registry supports both by implementing Docker's [content trust][docker-content-trust] model, and this article gets you started.</span><span class="sxs-lookup"><span data-stu-id="fa402-106">Azure Container Registry supports both by implementing Docker's [content trust][docker-content-trust] model, and this article gets you started.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa402-107">This feature is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="fa402-107">This feature is currently in preview.</span></span> <span data-ttu-id="fa402-108">Previews are made available to you on the condition that you agree to the [supplemental terms of use][terms-of-use].</span><span class="sxs-lookup"><span data-stu-id="fa402-108">Previews are made available to you on the condition that you agree to the [supplemental terms of use][terms-of-use].</span></span> <span data-ttu-id="fa402-109">Some aspects of this feature may change prior to general availability (GA).</span><span class="sxs-lookup"><span data-stu-id="fa402-109">Some aspects of this feature may change prior to general availability (GA).</span></span>

## <a name="how-content-trust-works"></a><span data-ttu-id="fa402-110">How content trust works</span><span class="sxs-lookup"><span data-stu-id="fa402-110">How content trust works</span></span>

<span data-ttu-id="fa402-111">As an image publisher, content trust allows you to **sign** the images you push to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-111">As an image publisher, content trust allows you to **sign** the images you push to your registry.</span></span> <span data-ttu-id="fa402-112">Consumers of your images (people or systems pulling images from your registry) can configure their clients to pull *only* signed images.</span><span class="sxs-lookup"><span data-stu-id="fa402-112">Consumers of your images (people or systems pulling images from your registry) can configure their clients to pull *only* signed images.</span></span> <span data-ttu-id="fa402-113">When an image consumer pulls a signed image, their Docker client verifies the integrity of the image.</span><span class="sxs-lookup"><span data-stu-id="fa402-113">When an image consumer pulls a signed image, their Docker client verifies the integrity of the image.</span></span> <span data-ttu-id="fa402-114">In this model, consumers are assured that the signed images in your registry were indeed published by you, and that they've not been modified since being published.</span><span class="sxs-lookup"><span data-stu-id="fa402-114">In this model, consumers are assured that the signed images in your registry were indeed published by you, and that they've not been modified since being published.</span></span>

### <a name="trusted-images"></a><span data-ttu-id="fa402-115">Trusted images</span><span class="sxs-lookup"><span data-stu-id="fa402-115">Trusted images</span></span>

<span data-ttu-id="fa402-116">Content trust works with the **tags** in a repository.</span><span class="sxs-lookup"><span data-stu-id="fa402-116">Content trust works with the **tags** in a repository.</span></span> <span data-ttu-id="fa402-117">Image repositories can contain images with both signed and unsigned tags.</span><span class="sxs-lookup"><span data-stu-id="fa402-117">Image repositories can contain images with both signed and unsigned tags.</span></span> <span data-ttu-id="fa402-118">For example, you might sign only the `myimage:stable` and `myimage:latest` images, but not `myimage:dev`.</span><span class="sxs-lookup"><span data-stu-id="fa402-118">For example, you might sign only the `myimage:stable` and `myimage:latest` images, but not `myimage:dev`.</span></span>

### <a name="signing-keys"></a><span data-ttu-id="fa402-119">Signing keys</span><span class="sxs-lookup"><span data-stu-id="fa402-119">Signing keys</span></span>

<span data-ttu-id="fa402-120">Content trust is managed through the use of a set of cryptographic signing keys.</span><span class="sxs-lookup"><span data-stu-id="fa402-120">Content trust is managed through the use of a set of cryptographic signing keys.</span></span> <span data-ttu-id="fa402-121">These keys are associated with a specific repository in a registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-121">These keys are associated with a specific repository in a registry.</span></span> <span data-ttu-id="fa402-122">There are several types of signing keys that Docker clients and your registry use in managing trust for the tags in a repository.</span><span class="sxs-lookup"><span data-stu-id="fa402-122">There are several types of signing keys that Docker clients and your registry use in managing trust for the tags in a repository.</span></span> <span data-ttu-id="fa402-123">When you enable content trust and integrate it into your container publishing and consumption pipeline, you must manage these keys carefully.</span><span class="sxs-lookup"><span data-stu-id="fa402-123">When you enable content trust and integrate it into your container publishing and consumption pipeline, you must manage these keys carefully.</span></span> <span data-ttu-id="fa402-124">For more information, see [Key management](#key-management) later in this article and [Manage keys for content trust][docker-manage-keys] in the Docker documentation.</span><span class="sxs-lookup"><span data-stu-id="fa402-124">For more information, see [Key management](#key-management) later in this article and [Manage keys for content trust][docker-manage-keys] in the Docker documentation.</span></span>

> [!TIP]
> <span data-ttu-id="fa402-125">This was a very high-level overview of Docker's content trust model.</span><span class="sxs-lookup"><span data-stu-id="fa402-125">This was a very high-level overview of Docker's content trust model.</span></span> <span data-ttu-id="fa402-126">For an in-depth discussion of content trust, see [Content trust in Docker][docker-content-trust].</span><span class="sxs-lookup"><span data-stu-id="fa402-126">For an in-depth discussion of content trust, see [Content trust in Docker][docker-content-trust].</span></span>

## <a name="enable-registry-content-trust"></a><span data-ttu-id="fa402-127">Enable registry content trust</span><span class="sxs-lookup"><span data-stu-id="fa402-127">Enable registry content trust</span></span>

<span data-ttu-id="fa402-128">Your first step is to enable content trust at the registry level.</span><span class="sxs-lookup"><span data-stu-id="fa402-128">Your first step is to enable content trust at the registry level.</span></span> <span data-ttu-id="fa402-129">Once you enable content trust, clients (users or services) can push signed images to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-129">Once you enable content trust, clients (users or services) can push signed images to your registry.</span></span> <span data-ttu-id="fa402-130">Enabling content trust on your registry does not restrict registry usage only to consumers with content trust enabled.</span><span class="sxs-lookup"><span data-stu-id="fa402-130">Enabling content trust on your registry does not restrict registry usage only to consumers with content trust enabled.</span></span> <span data-ttu-id="fa402-131">Consumers without content trust enabled can continue to use your registry as normal.</span><span class="sxs-lookup"><span data-stu-id="fa402-131">Consumers without content trust enabled can continue to use your registry as normal.</span></span> <span data-ttu-id="fa402-132">Consumers who have enabled content trust in their clients, however, will be able to see *only* signed images in your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-132">Consumers who have enabled content trust in their clients, however, will be able to see *only* signed images in your registry.</span></span>

<span data-ttu-id="fa402-133">To enable content trust for your registry, first navigate to the registry in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fa402-133">To enable content trust for your registry, first navigate to the registry in the Azure portal.</span></span> <span data-ttu-id="fa402-134">Under **POLICIES**, select **Content Trust (Preview)** > **Enabled** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="fa402-134">Under **POLICIES**, select **Content Trust (Preview)** > **Enabled** > **Save**.</span></span>

![Enabling content trust for a registry in the Azure portal][content-trust-01-portal]

## <a name="enable-client-content-trust"></a><span data-ttu-id="fa402-136">Enable client content trust</span><span class="sxs-lookup"><span data-stu-id="fa402-136">Enable client content trust</span></span>

<span data-ttu-id="fa402-137">To work with trusted images, both image publishers and consumers need to enable content trust for their Docker clients.</span><span class="sxs-lookup"><span data-stu-id="fa402-137">To work with trusted images, both image publishers and consumers need to enable content trust for their Docker clients.</span></span> <span data-ttu-id="fa402-138">As a publisher, you can sign the images you push to a content trust-enabled registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-138">As a publisher, you can sign the images you push to a content trust-enabled registry.</span></span> <span data-ttu-id="fa402-139">As a consumer, enabling content trust limits your view of a registry to signed images only.</span><span class="sxs-lookup"><span data-stu-id="fa402-139">As a consumer, enabling content trust limits your view of a registry to signed images only.</span></span> <span data-ttu-id="fa402-140">Content trust is disabled by default in Docker clients, but you can enable it per shell session or per command.</span><span class="sxs-lookup"><span data-stu-id="fa402-140">Content trust is disabled by default in Docker clients, but you can enable it per shell session or per command.</span></span>

<span data-ttu-id="fa402-141">To enable content trust for a shell session, set the `DOCKER_CONTENT_TRUST` environment variable to **1**.</span><span class="sxs-lookup"><span data-stu-id="fa402-141">To enable content trust for a shell session, set the `DOCKER_CONTENT_TRUST` environment variable to **1**.</span></span> <span data-ttu-id="fa402-142">For example, in the Bash shell:</span><span class="sxs-lookup"><span data-stu-id="fa402-142">For example, in the Bash shell:</span></span>

```bash
# Enable content trust for shell session
export DOCKER_CONTENT_TRUST=1
```

<span data-ttu-id="fa402-143">If instead you'd like to enable or disable content trust for a single command, several Docker commands support the `--disable-content-trust` argument.</span><span class="sxs-lookup"><span data-stu-id="fa402-143">If instead you'd like to enable or disable content trust for a single command, several Docker commands support the `--disable-content-trust` argument.</span></span> <span data-ttu-id="fa402-144">To enable content trust for a single command:</span><span class="sxs-lookup"><span data-stu-id="fa402-144">To enable content trust for a single command:</span></span>

```bash
# Enable content trust for single command
docker build --disable-content-trust=false -t myacr.azurecr.io/myimage:v1 .
```

<span data-ttu-id="fa402-145">If you've enabled content trust for your shell session and want to disable it for a single command:</span><span class="sxs-lookup"><span data-stu-id="fa402-145">If you've enabled content trust for your shell session and want to disable it for a single command:</span></span>

```bash
# Disable content trust for single command
docker build --disable-content-trust -t myacr.azurecr.io/myimage:v1 .
```

## <a name="grant-image-signing-permissions"></a><span data-ttu-id="fa402-146">Grant image signing permissions</span><span class="sxs-lookup"><span data-stu-id="fa402-146">Grant image signing permissions</span></span>

<span data-ttu-id="fa402-147">Only the users or systems you've granted permission can push trusted images to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-147">Only the users or systems you've granted permission can push trusted images to your registry.</span></span> <span data-ttu-id="fa402-148">To grant trusted image push permission to a user (or a system using a service principal), grant their Azure Active Directory identities the `AcrImageSigner` role.</span><span class="sxs-lookup"><span data-stu-id="fa402-148">To grant trusted image push permission to a user (or a system using a service principal), grant their Azure Active Directory identities the `AcrImageSigner` role.</span></span> <span data-ttu-id="fa402-149">This is in addition to the `Contributor` (or `Owner`) role required for pushing images to the registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-149">This is in addition to the `Contributor` (or `Owner`) role required for pushing images to the registry.</span></span>

<span data-ttu-id="fa402-150">Details for granting the `AcrImageSigner` role in the Azure portal and the Azure CLI follow.</span><span class="sxs-lookup"><span data-stu-id="fa402-150">Details for granting the `AcrImageSigner` role in the Azure portal and the Azure CLI follow.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="fa402-151">Azure portal</span><span class="sxs-lookup"><span data-stu-id="fa402-151">Azure portal</span></span>

<span data-ttu-id="fa402-152">Navigate to your registry in the Azure portal, then select **Access Control (IAM)** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="fa402-152">Navigate to your registry in the Azure portal, then select **Access Control (IAM)** > **Add**.</span></span> <span data-ttu-id="fa402-153">Under **Add permissions**, select `AcrImageSigner` under **Role**, then **Select** one or more users or service principals, then **Save**.</span><span class="sxs-lookup"><span data-stu-id="fa402-153">Under **Add permissions**, select `AcrImageSigner` under **Role**, then **Select** one or more users or service principals, then **Save**.</span></span>

<span data-ttu-id="fa402-154">In this example, two entities have been assigned the `AcrImageSigner` role: a service principal named "service-principal," and a user named "Azure User."</span><span class="sxs-lookup"><span data-stu-id="fa402-154">In this example, two entities have been assigned the `AcrImageSigner` role: a service principal named "service-principal," and a user named "Azure User."</span></span>

![Enabling content trust for a registry in the Azure portal][content-trust-02-portal]

### <a name="azure-cli"></a><span data-ttu-id="fa402-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fa402-156">Azure CLI</span></span>

<span data-ttu-id="fa402-157">To grant signing permissions to a user with the Azure CLI, assign the `AcrImageSigner` role to the user, scoped to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-157">To grant signing permissions to a user with the Azure CLI, assign the `AcrImageSigner` role to the user, scoped to your registry.</span></span> <span data-ttu-id="fa402-158">The format of the command is:</span><span class="sxs-lookup"><span data-stu-id="fa402-158">The format of the command is:</span></span>

```azurecli
az role assignment create --scope <registry ID> --role AcrImageSigner --assignee <user name>
```

<span data-ttu-id="fa402-159">For example, to grant yourself the role, you can run the following commands in an authenticated Azure CLI session.</span><span class="sxs-lookup"><span data-stu-id="fa402-159">For example, to grant yourself the role, you can run the following commands in an authenticated Azure CLI session.</span></span> <span data-ttu-id="fa402-160">Modify the `REGISTRY` value to reflect the name of your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-160">Modify the `REGISTRY` value to reflect the name of your Azure container registry.</span></span>

```bash
# Grant signing permissions to authenticated Azure CLI user
REGISTRY=myregistry
USER=$(az account show --query user.name --output tsv)
REGISTRY_ID=$(az acr show --name $REGISTRY --query id --output tsv)

az role assignment create --scope $REGISTRY_ID --role AcrImageSigner --assignee $USER
```

<span data-ttu-id="fa402-161">You can also grant a [service principal](container-registry-auth-service-principal.md) the rights to push trusted images to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-161">You can also grant a [service principal](container-registry-auth-service-principal.md) the rights to push trusted images to your registry.</span></span> <span data-ttu-id="fa402-162">Using a service principal is useful for build systems and other unattended systems that need to push trusted images to your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-162">Using a service principal is useful for build systems and other unattended systems that need to push trusted images to your registry.</span></span> <span data-ttu-id="fa402-163">The format is similar to granting a user permission, but specify a service principal ID for the `--assignee` value.</span><span class="sxs-lookup"><span data-stu-id="fa402-163">The format is similar to granting a user permission, but specify a service principal ID for the `--assignee` value.</span></span>

```azurecli
az role assignment create --scope $REGISTRY_ID --role AcrImageSigner --assignee <service principal ID>
```

<span data-ttu-id="fa402-164">The `<service principal ID>` can be the service principal's **appId**, **objectId**, or one of its **servicePrincipalNames**.</span><span class="sxs-lookup"><span data-stu-id="fa402-164">The `<service principal ID>` can be the service principal's **appId**, **objectId**, or one of its **servicePrincipalNames**.</span></span> <span data-ttu-id="fa402-165">For more information about working with service principals and Azure Container Registry, see [Azure Container Registry authentication with service principals](container-registry-auth-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="fa402-165">For more information about working with service principals and Azure Container Registry, see [Azure Container Registry authentication with service principals](container-registry-auth-service-principal.md).</span></span>

## <a name="push-a-trusted-image"></a><span data-ttu-id="fa402-166">Push a trusted image</span><span class="sxs-lookup"><span data-stu-id="fa402-166">Push a trusted image</span></span>

<span data-ttu-id="fa402-167">To push a trusted image tag to your container registry, enable content trust and push the image with `docker push`.</span><span class="sxs-lookup"><span data-stu-id="fa402-167">To push a trusted image tag to your container registry, enable content trust and push the image with `docker push`.</span></span> <span data-ttu-id="fa402-168">The first time you push a signed tag, you're asked to create a passphrase for both a root signing key and a repository signing key.</span><span class="sxs-lookup"><span data-stu-id="fa402-168">The first time you push a signed tag, you're asked to create a passphrase for both a root signing key and a repository signing key.</span></span> <span data-ttu-id="fa402-169">Both the root and repository keys are generated and stored locally on your machine.</span><span class="sxs-lookup"><span data-stu-id="fa402-169">Both the root and repository keys are generated and stored locally on your machine.</span></span>

```console
$ docker push myregistry.azurecr.io/myimage:v1
The push refers to repository [myregistry.azurecr.io/myimage]
ee83fc5847cb: Pushed
v1: digest: sha256:aca41a608e5eb015f1ec6755f490f3be26b48010b178e78c00eac21ffbe246f1 size: 524
Signing and pushing trust metadata
You are about to create a new root signing key passphrase. This passphrase
will be used to protect the most sensitive key in your signing system. Please
choose a long, complex passphrase and be careful to keep the password and the
key file itself secure and backed up. It is highly recommended that you use a
password manager to generate the passphrase and keep it safe. There will be no
way to recover this key. You can find the key in your config directory.
Enter passphrase for new root key with ID 4c6c56a:
Repeat passphrase for new root key with ID 4c6c56a:
Enter passphrase for new repository key with ID bcd6d98:
Repeat passphrase for new repository key with ID bcd6d98:
Finished initializing "myregistry.azurecr.io/myimage"
Successfully signed myregistry.azurecr.io/myimage:v1
```

<span data-ttu-id="fa402-170">After your first `docker push` with content trust enabled, the Docker client uses the same root key for subsequent pushes.</span><span class="sxs-lookup"><span data-stu-id="fa402-170">After your first `docker push` with content trust enabled, the Docker client uses the same root key for subsequent pushes.</span></span> <span data-ttu-id="fa402-171">On each subsequent push to the same repository, you're asked only for the repository key.</span><span class="sxs-lookup"><span data-stu-id="fa402-171">On each subsequent push to the same repository, you're asked only for the repository key.</span></span> <span data-ttu-id="fa402-172">Each time you push a trusted image to a new repository, you're asked to supply a passphrase for a new repository key.</span><span class="sxs-lookup"><span data-stu-id="fa402-172">Each time you push a trusted image to a new repository, you're asked to supply a passphrase for a new repository key.</span></span>

## <a name="pull-a-trusted-image"></a><span data-ttu-id="fa402-173">Pull a trusted image</span><span class="sxs-lookup"><span data-stu-id="fa402-173">Pull a trusted image</span></span>

<span data-ttu-id="fa402-174">To pull a trusted image, enable content trust and run the `docker pull` command as normal.</span><span class="sxs-lookup"><span data-stu-id="fa402-174">To pull a trusted image, enable content trust and run the `docker pull` command as normal.</span></span> <span data-ttu-id="fa402-175">Consumers with content trust enabled can pull only images with signed tags.</span><span class="sxs-lookup"><span data-stu-id="fa402-175">Consumers with content trust enabled can pull only images with signed tags.</span></span> <span data-ttu-id="fa402-176">Here's an example of pulling a signed tag:</span><span class="sxs-lookup"><span data-stu-id="fa402-176">Here's an example of pulling a signed tag:</span></span>

```console
$ docker pull myregistry.azurecr.io/myimage:signed
Pull (1 of 1): myregistry.azurecr.io/myimage:signed@sha256:0800d17e37fb4f8194495b1a188f121e5b54efb52b5d93dc9e0ed97fce49564b
sha256:0800d17e37fb4f8194495b1a188f121e5b54efb52b5d93dc9e0ed97fce49564b: Pulling from myimage
8e3ba11ec2a2: Pull complete
Digest: sha256:0800d17e37fb4f8194495b1a188f121e5b54efb52b5d93dc9e0ed97fce49564b
Status: Downloaded newer image for myregistry.azurecr.io/myimage@sha256:0800d17e37fb4f8194495b1a188f121e5b54efb52b5d93dc9e0ed97fce49564b
Tagging myregistry.azurecr.io/myimage@sha256:0800d17e37fb4f8194495b1a188f121e5b54efb52b5d93dc9e0ed97fce49564b as myregistry.azurecr.io/myimage:signed
```

<span data-ttu-id="fa402-177">If a client with content trust enabled tries to pull an unsigned tag, the operation fails:</span><span class="sxs-lookup"><span data-stu-id="fa402-177">If a client with content trust enabled tries to pull an unsigned tag, the operation fails:</span></span>

```console
$ docker pull myregistry.azurecr.io/myimage:unsigned
No valid trust data for unsigned
```

### <a name="behind-the-scenes"></a><span data-ttu-id="fa402-178">Behind the scenes</span><span class="sxs-lookup"><span data-stu-id="fa402-178">Behind the scenes</span></span>

<span data-ttu-id="fa402-179">When you run `docker pull`, the Docker client uses the same library as in the [Notary CLI][docker-notary-cli] to request the tag-to-SHA-256 digest mapping for the tag you're pulling.</span><span class="sxs-lookup"><span data-stu-id="fa402-179">When you run `docker pull`, the Docker client uses the same library as in the [Notary CLI][docker-notary-cli] to request the tag-to-SHA-256 digest mapping for the tag you're pulling.</span></span> <span data-ttu-id="fa402-180">After validating the signatures on the trust data, the client instructs Docker Engine to do a "pull by digest."</span><span class="sxs-lookup"><span data-stu-id="fa402-180">After validating the signatures on the trust data, the client instructs Docker Engine to do a "pull by digest."</span></span> <span data-ttu-id="fa402-181">During the pull, the Engine uses the SHA-256 checksum as a content address to request and validate the image manifest from the Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-181">During the pull, the Engine uses the SHA-256 checksum as a content address to request and validate the image manifest from the Azure container registry.</span></span>

## <a name="key-management"></a><span data-ttu-id="fa402-182">Key management</span><span class="sxs-lookup"><span data-stu-id="fa402-182">Key management</span></span>

<span data-ttu-id="fa402-183">As stated in the `docker push` output when you push your first trusted image, the root key is the most sensitive.</span><span class="sxs-lookup"><span data-stu-id="fa402-183">As stated in the `docker push` output when you push your first trusted image, the root key is the most sensitive.</span></span> <span data-ttu-id="fa402-184">Be sure to back up your root key and store it in a secure location.</span><span class="sxs-lookup"><span data-stu-id="fa402-184">Be sure to back up your root key and store it in a secure location.</span></span> <span data-ttu-id="fa402-185">By default, the Docker client stores signing keys in the following directory:</span><span class="sxs-lookup"><span data-stu-id="fa402-185">By default, the Docker client stores signing keys in the following directory:</span></span>

```sh
~/.docker/trust/private
```

<span data-ttu-id="fa402-186">Back up your root and repository keys by compressing them in an archive and storing it securely offline (such as on a USB storage device).</span><span class="sxs-lookup"><span data-stu-id="fa402-186">Back up your root and repository keys by compressing them in an archive and storing it securely offline (such as on a USB storage device).</span></span> <span data-ttu-id="fa402-187">For example, in Bash:</span><span class="sxs-lookup"><span data-stu-id="fa402-187">For example, in Bash:</span></span>

```bash
umask 077; tar -zcvf docker_private_keys_backup.tar.gz ~/.docker/trust/private; umask 022
```

<span data-ttu-id="fa402-188">Along with the locally generated root and repository keys, several others are generated and stored by Azure Container Registry when you push a trusted image.</span><span class="sxs-lookup"><span data-stu-id="fa402-188">Along with the locally generated root and repository keys, several others are generated and stored by Azure Container Registry when you push a trusted image.</span></span> <span data-ttu-id="fa402-189">For a detailed discussion of the various keys in Docker's content trust implementation, including additional management guidance, see [Manage keys for content trust][docker-manage-keys] in the Docker documentation.</span><span class="sxs-lookup"><span data-stu-id="fa402-189">For a detailed discussion of the various keys in Docker's content trust implementation, including additional management guidance, see [Manage keys for content trust][docker-manage-keys] in the Docker documentation.</span></span>

### <a name="lost-root-key"></a><span data-ttu-id="fa402-190">Lost root key</span><span class="sxs-lookup"><span data-stu-id="fa402-190">Lost root key</span></span>

<span data-ttu-id="fa402-191">If you lose access to your root key, you lose access to the signed tags in any repository whose tags were signed with that key.</span><span class="sxs-lookup"><span data-stu-id="fa402-191">If you lose access to your root key, you lose access to the signed tags in any repository whose tags were signed with that key.</span></span> <span data-ttu-id="fa402-192">Azure Container Registry cannot restore access to image tags signed with a lost root key.</span><span class="sxs-lookup"><span data-stu-id="fa402-192">Azure Container Registry cannot restore access to image tags signed with a lost root key.</span></span> <span data-ttu-id="fa402-193">To remove all trust data (signatures) for your registry, first disable, then re-enable content trust for the registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-193">To remove all trust data (signatures) for your registry, first disable, then re-enable content trust for the registry.</span></span>

> [!WARNING]
> <span data-ttu-id="fa402-194">Disabling and re-enabling content trust in your registry **deletes all trust data for all signed tags in every repository in your registry**.</span><span class="sxs-lookup"><span data-stu-id="fa402-194">Disabling and re-enabling content trust in your registry **deletes all trust data for all signed tags in every repository in your registry**.</span></span> <span data-ttu-id="fa402-195">This action is irreversible--Azure Container Registry cannot recover deleted trust data.</span><span class="sxs-lookup"><span data-stu-id="fa402-195">This action is irreversible--Azure Container Registry cannot recover deleted trust data.</span></span> <span data-ttu-id="fa402-196">Disabling content trust does not delete the images themselves.</span><span class="sxs-lookup"><span data-stu-id="fa402-196">Disabling content trust does not delete the images themselves.</span></span>

<span data-ttu-id="fa402-197">To disable content trust for your registry, navigate to the registry in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fa402-197">To disable content trust for your registry, navigate to the registry in the Azure portal.</span></span> <span data-ttu-id="fa402-198">Under **POLICIES**, select **Content Trust (Preview)** > **Disabled** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="fa402-198">Under **POLICIES**, select **Content Trust (Preview)** > **Disabled** > **Save**.</span></span> <span data-ttu-id="fa402-199">You're warned of the loss of all signatures in the registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-199">You're warned of the loss of all signatures in the registry.</span></span> <span data-ttu-id="fa402-200">Select **OK** to permanently delete all signatures in your registry.</span><span class="sxs-lookup"><span data-stu-id="fa402-200">Select **OK** to permanently delete all signatures in your registry.</span></span>

![Disabling content trust for a registry in the Azure portal][content-trust-03-portal]

## <a name="next-steps"></a><span data-ttu-id="fa402-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa402-202">Next steps</span></span>

<span data-ttu-id="fa402-203">See the Docker documentation for additional information about content trust.</span><span class="sxs-lookup"><span data-stu-id="fa402-203">See the Docker documentation for additional information about content trust.</span></span> <span data-ttu-id="fa402-204">While several key points were touched on in this article, content trust is an extensive topic and is covered more in-depth in the Docker documentation.</span><span class="sxs-lookup"><span data-stu-id="fa402-204">While several key points were touched on in this article, content trust is an extensive topic and is covered more in-depth in the Docker documentation.</span></span>

<span data-ttu-id="fa402-205">[Content trust in Docker][docker-content-trust]</span><span class="sxs-lookup"><span data-stu-id="fa402-205">[Content trust in Docker][docker-content-trust]</span></span>

<!-- IMAGES> -->
[content-trust-01-portal]: ./media/container-registry-content-trust/content-trust-01-portal.png
[content-trust-02-portal]: ./media/container-registry-content-trust/content-trust-02-portal.png
[content-trust-03-portal]: ./media/container-registry-content-trust/content-trust-03-portal.png

<!-- LINKS - external -->
[docker-content-trust]: https://docs.docker.com/engine/security/trust/content_trust
[docker-manage-keys]: https://docs.docker.com/engine/security/trust/trust_key_mng/
[docker-notary-cli]: https://docs.docker.com/notary/getting_started/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[terms-of-use]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/

<!-- LINKS - internal -->
[azure-cli]: /cli/azure/install-azure-cli
