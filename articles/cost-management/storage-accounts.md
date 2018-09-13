---
title: Configure storage accounts for Azure Cost Management | Microsoft Docs
description: This article describes how you configure Azure storage accounts and AWS storage buckets for Azure Cost Management.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/07/2018
ms.topic: conceptual
ms.service: cost-management
manager: carmonm
ms.custom: ''
ms.openlocfilehash: af976d1af2f777c60e6a4fe7bd5c2e9369a9eac7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864598"
---
# <a name="configure-storage-accounts-for-cost-management"></a><span data-ttu-id="dfc5c-103">Configure storage accounts for Cost Management</span><span class="sxs-lookup"><span data-stu-id="dfc5c-103">Configure storage accounts for Cost Management</span></span>

<!--- intent: As a Cost Management user, I want to configure Cost Management to use my cloud service provider storage account to store my reports. -->

<span data-ttu-id="dfc5c-104">You can save Cost Management reports in the Cloudyn portal, Azure storage, or AWS storage buckets.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-104">You can save Cost Management reports in the Cloudyn portal, Azure storage, or AWS storage buckets.</span></span> <span data-ttu-id="dfc5c-105">Saving your reports to the Cloudyn portal is free of charge.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-105">Saving your reports to the Cloudyn portal is free of charge.</span></span> <span data-ttu-id="dfc5c-106">However, saving your reports to your cloud service provider's storage is optional and incurs additional cost.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-106">However, saving your reports to your cloud service provider's storage is optional and incurs additional cost.</span></span> <span data-ttu-id="dfc5c-107">This article helps you configure Azure storage accounts and Amazon Web Services (AWS) storage buckets to store your reports.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-107">This article helps you configure Azure storage accounts and Amazon Web Services (AWS) storage buckets to store your reports.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfc5c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dfc5c-108">Prerequisites</span></span>

<span data-ttu-id="dfc5c-109">You must have either an Azure storage account or an Amazon storage bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-109">You must have either an Azure storage account or an Amazon storage bucket.</span></span>

<span data-ttu-id="dfc5c-110">If you don't have an Azure storage account, you need to create one.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-110">If you don't have an Azure storage account, you need to create one.</span></span> <span data-ttu-id="dfc5c-111">For more information about creating an Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="dfc5c-111">For more information about creating an Azure storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span>

<span data-ttu-id="dfc5c-112">If you don't have an AWS simple storage service (S3) bucket, you need to create one.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-112">If you don't have an AWS simple storage service (S3) bucket, you need to create one.</span></span> <span data-ttu-id="dfc5c-113">For more information about creating an S3 bucket, see [Create a Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).</span><span class="sxs-lookup"><span data-stu-id="dfc5c-113">For more information about creating an S3 bucket, see [Create a Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).</span></span>

## <a name="configure-your-azure-storage-account"></a><span data-ttu-id="dfc5c-114">Configure your Azure storage account</span><span class="sxs-lookup"><span data-stu-id="dfc5c-114">Configure your Azure storage account</span></span>

<span data-ttu-id="dfc5c-115">Configuring you Azure storage for use by Cost Management is straightforward.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-115">Configuring you Azure storage for use by Cost Management is straightforward.</span></span> <span data-ttu-id="dfc5c-116">Gather details about the storage account and copy them in the Cloudyn portal.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-116">Gather details about the storage account and copy them in the Cloudyn portal.</span></span>

1. <span data-ttu-id="dfc5c-117">Sign in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-117">Sign in to the Azure portal at http://portal.azure.com.</span></span>
2. <span data-ttu-id="dfc5c-118">Click **All Services**, select **Storage accounts**, scroll to the storage account that you want to use, and then select the account.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-118">Click **All Services**, select **Storage accounts**, scroll to the storage account that you want to use, and then select the account.</span></span>
3. <span data-ttu-id="dfc5c-119">On your storage account page under **Settings**, click **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-119">On your storage account page under **Settings**, click **Access Keys**.</span></span>
4. <span data-ttu-id="dfc5c-120">Copy your **Storage account name** and **Connection string** under key1.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-120">Copy your **Storage account name** and **Connection string** under key1.</span></span>  
<span data-ttu-id="dfc5c-121">![Azure storage access keys](./media/storage-accounts/azure-storage-access-keys.png)</span><span class="sxs-lookup"><span data-stu-id="dfc5c-121">![Azure storage access keys](./media/storage-accounts/azure-storage-access-keys.png)</span></span>  
5. <span data-ttu-id="dfc5c-122">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com and sign in.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-122">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com and sign in.</span></span>
6. <span data-ttu-id="dfc5c-123">Click the cog symbol and then select **Reports Storage Management**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-123">Click the cog symbol and then select **Reports Storage Management**.</span></span>
7. <span data-ttu-id="dfc5c-124">Click **Add new +** and ensure that Microsoft Azure is selected.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-124">Click **Add new +** and ensure that Microsoft Azure is selected.</span></span> <span data-ttu-id="dfc5c-125">Paste your Azure storage account name in the **Name** area.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-125">Paste your Azure storage account name in the **Name** area.</span></span> <span data-ttu-id="dfc5c-126">Paste your **connection string** in the corresponding area.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-126">Paste your **connection string** in the corresponding area.</span></span> <span data-ttu-id="dfc5c-127">Enter a container name and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-127">Enter a container name and then click **Save**.</span></span>  
<span data-ttu-id="dfc5c-128">![Cloudyn storage configured for Azure](./media/storage-accounts/azure-cloudyn-storage.png)</span><span class="sxs-lookup"><span data-stu-id="dfc5c-128">![Cloudyn storage configured for Azure](./media/storage-accounts/azure-cloudyn-storage.png)</span></span>

  <span data-ttu-id="dfc5c-129">Your new Azure report storage entry appears in the storage account list.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-129">Your new Azure report storage entry appears in the storage account list.</span></span>  
    ![New Azure report storage in list](./media/storage-accounts/azure-storage-entry.png)


<span data-ttu-id="dfc5c-131">You can now save reports to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-131">You can now save reports to Azure storage.</span></span> <span data-ttu-id="dfc5c-132">In any report, click **Actions** and then select **Schedule report**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-132">In any report, click **Actions** and then select **Schedule report**.</span></span> <span data-ttu-id="dfc5c-133">Name the report and then either add your own URL or use the automatically created URL.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-133">Name the report and then either add your own URL or use the automatically created URL.</span></span> <span data-ttu-id="dfc5c-134">Select  **Save to storage**  and then select the storage account.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-134">Select  **Save to storage**  and then select the storage account.</span></span> <span data-ttu-id="dfc5c-135">Enter a prefix that gets appended to the report file name.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-135">Enter a prefix that gets appended to the report file name.</span></span> <span data-ttu-id="dfc5c-136">Select either CSV or JSON file format and then save the report.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-136">Select either CSV or JSON file format and then save the report.</span></span>

## <a name="configure-an-aws-storage-bucket"></a><span data-ttu-id="dfc5c-137">Configure an AWS storage bucket</span><span class="sxs-lookup"><span data-stu-id="dfc5c-137">Configure an AWS storage bucket</span></span>

<span data-ttu-id="dfc5c-138">The Cloudyn uses existing AWS credentials: User or Role, to save the reports to your bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-138">The Cloudyn uses existing AWS credentials: User or Role, to save the reports to your bucket.</span></span> <span data-ttu-id="dfc5c-139">To test the access, Cloudyn tries to save a small text file to the bucket with the file name _check-bucket-permission.txt_.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-139">To test the access, Cloudyn tries to save a small text file to the bucket with the file name _check-bucket-permission.txt_.</span></span>

<span data-ttu-id="dfc5c-140">You provide the Cloudyn role or user with the PutObject permission to your bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-140">You provide the Cloudyn role or user with the PutObject permission to your bucket.</span></span> <span data-ttu-id="dfc5c-141">Then, use an existing bucket or create a new one to save reports.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-141">Then, use an existing bucket or create a new one to save reports.</span></span> <span data-ttu-id="dfc5c-142">Finally, decide how to manage the storage class, set lifecycle rules, or remove any unnecessary files.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-142">Finally, decide how to manage the storage class, set lifecycle rules, or remove any unnecessary files.</span></span>

###  <a name="assign-permissions-to-your-aws-user-or-role"></a><span data-ttu-id="dfc5c-143">Assign permissions to your AWS user or role</span><span class="sxs-lookup"><span data-stu-id="dfc5c-143">Assign permissions to your AWS user or role</span></span>

<span data-ttu-id="dfc5c-144">When you create a new policy, you provide the exact permissions needed to save a report to a S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-144">When you create a new policy, you provide the exact permissions needed to save a report to a S3 bucket.</span></span>

1. <span data-ttu-id="dfc5c-145">Sign in to the AWS console and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-145">Sign in to the AWS console and select **Services**.</span></span>
2. <span data-ttu-id="dfc5c-146">Select **IAM** from the list of services.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-146">Select **IAM** from the list of services.</span></span>
3. <span data-ttu-id="dfc5c-147">Select **Policies** on the left side of the console and then click **Create Policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-147">Select **Policies** on the left side of the console and then click **Create Policy**.</span></span>
4. <span data-ttu-id="dfc5c-148">Click the **JSON** tab.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-148">Click the **JSON** tab.</span></span>
5. <span data-ttu-id="dfc5c-149">The following policy allows you to save a report to a S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-149">The following policy allows you to save a report to a S3 bucket.</span></span> <span data-ttu-id="dfc5c-150">Copy and paste the following policy example to the **JSON** tab. Replace &lt;bucketname&gt; with your bucket name.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-150">Copy and paste the following policy example to the **JSON** tab. Replace &lt;bucketname&gt; with your bucket name.</span></span>

  ```
{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid":  "CloudynSaveReport2S3",
        "Effect":      "Allow",
        "Action": [
          "s3:PutObject"
        ],
        "Resource": [
          "arn:aws:s3:::<bucketname>/*"
        ]
      }
    ]
}
```

6. <span data-ttu-id="dfc5c-151">Click **Review policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-151">Click **Review policy**.</span></span>  
    <span data-ttu-id="dfc5c-152">![Review policy](./media/storage-accounts/aws-policy.png)</span><span class="sxs-lookup"><span data-stu-id="dfc5c-152">![Review policy](./media/storage-accounts/aws-policy.png)</span></span>  
7. <span data-ttu-id="dfc5c-153">On the Review policy page, type a name for your policy.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-153">On the Review policy page, type a name for your policy.</span></span> <span data-ttu-id="dfc5c-154">For example, _CloudynSaveReport2S3_.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-154">For example, _CloudynSaveReport2S3_.</span></span>
8. <span data-ttu-id="dfc5c-155">Click **Create policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-155">Click **Create policy**.</span></span>

### <a name="attach-the-policy-to-a-cloudyn-role-or-user-in-your-account"></a><span data-ttu-id="dfc5c-156">Attach the policy to a Cloudyn role or user in your account</span><span class="sxs-lookup"><span data-stu-id="dfc5c-156">Attach the policy to a Cloudyn role or user in your account</span></span>

<span data-ttu-id="dfc5c-157">To attach the new policy, you open the AWS console and edit the Cloudyn role or user.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-157">To attach the new policy, you open the AWS console and edit the Cloudyn role or user.</span></span>

1. <span data-ttu-id="dfc5c-158">Sign in to the AWS console and select **Services**, then select **IAM** from the list of services.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-158">Sign in to the AWS console and select **Services**, then select **IAM** from the list of services.</span></span>
2. <span data-ttu-id="dfc5c-159">Select either **Roles** or **Users** from the left side of the console.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-159">Select either **Roles** or **Users** from the left side of the console.</span></span>

<span data-ttu-id="dfc5c-160">**For roles:**</span><span class="sxs-lookup"><span data-stu-id="dfc5c-160">**For roles:**</span></span>

  1. <span data-ttu-id="dfc5c-161">Click your Cloudyn role name.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-161">Click your Cloudyn role name.</span></span>
  2. <span data-ttu-id="dfc5c-162">On the **Permissions** tab, click **Attach Policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-162">On the **Permissions** tab, click **Attach Policy**.</span></span>
  3. <span data-ttu-id="dfc5c-163">Search for the policy that you created and select it, then click **Attach Policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-163">Search for the policy that you created and select it, then click **Attach Policy**.</span></span>
    <span data-ttu-id="dfc5c-164">![AWS - Attach policy for a role](./media/storage-accounts/aws-attach-policy-role.png)</span><span class="sxs-lookup"><span data-stu-id="dfc5c-164">![AWS - Attach policy for a role](./media/storage-accounts/aws-attach-policy-role.png)</span></span>

<span data-ttu-id="dfc5c-165">**For users:**</span><span class="sxs-lookup"><span data-stu-id="dfc5c-165">**For users:**</span></span>

1. <span data-ttu-id="dfc5c-166">Select the Cloudyn User.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-166">Select the Cloudyn User.</span></span>
2. <span data-ttu-id="dfc5c-167">On the **Permissions** tab, click **Add permissions**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-167">On the **Permissions** tab, click **Add permissions**.</span></span>
3. <span data-ttu-id="dfc5c-168">In the **Grant Permission** section, select **Attach existing policies directly**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-168">In the **Grant Permission** section, select **Attach existing policies directly**.</span></span>
4. <span data-ttu-id="dfc5c-169">Search for the policy that you created and select it, then click **Next: Review**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-169">Search for the policy that you created and select it, then click **Next: Review**.</span></span>
5. <span data-ttu-id="dfc5c-170">On the Add permissions to role name page, click **Add permissions**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-170">On the Add permissions to role name page, click **Add permissions**.</span></span>  
    <span data-ttu-id="dfc5c-171">![AWS - Attach policy for a user](./media/storage-accounts/aws-attach-policy-user.png)</span><span class="sxs-lookup"><span data-stu-id="dfc5c-171">![AWS - Attach policy for a user](./media/storage-accounts/aws-attach-policy-user.png)</span></span>


### <a name="optional-set-permission-with-bucket-policy"></a><span data-ttu-id="dfc5c-172">Optional: Set permission with bucket policy</span><span class="sxs-lookup"><span data-stu-id="dfc5c-172">Optional: Set permission with bucket policy</span></span>

<span data-ttu-id="dfc5c-173">You can also set permission to create reports on your S3 bucket using a bucket policy.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-173">You can also set permission to create reports on your S3 bucket using a bucket policy.</span></span> <span data-ttu-id="dfc5c-174">In the classic S3 view:</span><span class="sxs-lookup"><span data-stu-id="dfc5c-174">In the classic S3 view:</span></span>

1. <span data-ttu-id="dfc5c-175">Create or select an existing bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-175">Create or select an existing bucket.</span></span>
2. <span data-ttu-id="dfc5c-176">Select the **Permissions** tab and then click **Bucket policy**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-176">Select the **Permissions** tab and then click **Bucket policy**.</span></span>
3. <span data-ttu-id="dfc5c-177">Copy and paste the following policy sample.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-177">Copy and paste the following policy sample.</span></span> <span data-ttu-id="dfc5c-178">Replace &lt;bucket\_name&gt; and &lt;Cloudyn\_principle&gt; with the ARN of your bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-178">Replace &lt;bucket\_name&gt; and &lt;Cloudyn\_principle&gt; with the ARN of your bucket.</span></span> <span data-ttu-id="dfc5c-179">Replace the ARN of either the role or user used by Cloudyn.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-179">Replace the ARN of either the role or user used by Cloudyn.</span></span>

  ```
{
  "Id": "Policy1485775646248",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SaveReport2S3",
      "Action": [
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": "<bucket_name>/*",
      "Principal": {
        "AWS": [
          "<Cloudyn_principle>"
        ]
      }
    }
  ]
}
```

4. <span data-ttu-id="dfc5c-180">In the Bucket policy editor, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-180">In the Bucket policy editor, click **Save**.</span></span>

### <a name="add-aws-report-storage-to-cloudyn"></a><span data-ttu-id="dfc5c-181">Add AWS report storage to Cloudyn</span><span class="sxs-lookup"><span data-stu-id="dfc5c-181">Add AWS report storage to Cloudyn</span></span>

1. <span data-ttu-id="dfc5c-182">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com and sign in.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-182">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com and sign in.</span></span>
2. <span data-ttu-id="dfc5c-183">Click the cog symbol and then select **Reports Storage Management**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-183">Click the cog symbol and then select **Reports Storage Management**.</span></span>
3. <span data-ttu-id="dfc5c-184">Click **Add new +** and ensure that AWS is selected.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-184">Click **Add new +** and ensure that AWS is selected.</span></span>
4. <span data-ttu-id="dfc5c-185">Select an account and storage bucket.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-185">Select an account and storage bucket.</span></span> <span data-ttu-id="dfc5c-186">The name of the AWS storage bucket is automatically filled-in.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-186">The name of the AWS storage bucket is automatically filled-in.</span></span>  
    ![Add report storage for AWS bucket](./media/storage-accounts/aws-cloudyn-storage.png)  
5. <span data-ttu-id="dfc5c-188">Click **Save** and then click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-188">Click **Save** and then click **Ok**.</span></span>

    <span data-ttu-id="dfc5c-189">Your new AWS report storage entry appears in the storage account list.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-189">Your new AWS report storage entry appears in the storage account list.</span></span>  
    ![New AWS report storage in list](./media/storage-accounts/aws-storage-entry.png)


<span data-ttu-id="dfc5c-191">You can now save reports to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-191">You can now save reports to Azure storage.</span></span> <span data-ttu-id="dfc5c-192">In any report, click **Actions**  and then select **Schedule report**.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-192">In any report, click **Actions**  and then select **Schedule report**.</span></span> <span data-ttu-id="dfc5c-193">Name the report and then either add your own URL or use the automatically created URL.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-193">Name the report and then either add your own URL or use the automatically created URL.</span></span> <span data-ttu-id="dfc5c-194">Select  **Save to storage**  and then select the storage account.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-194">Select  **Save to storage**  and then select the storage account.</span></span> <span data-ttu-id="dfc5c-195">Enter a prefix that gets appended to the report file name.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-195">Enter a prefix that gets appended to the report file name.</span></span> <span data-ttu-id="dfc5c-196">Select either CSV or JSON file format and then save the report.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-196">Select either CSV or JSON file format and then save the report.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc5c-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="dfc5c-197">Next steps</span></span>

- <span data-ttu-id="dfc5c-198">Review [Understanding cost management reports](understanding-cost-reports.md) to learn about the basic structure and functions of cost management reports.</span><span class="sxs-lookup"><span data-stu-id="dfc5c-198">Review [Understanding cost management reports](understanding-cost-reports.md) to learn about the basic structure and functions of cost management reports.</span></span>
