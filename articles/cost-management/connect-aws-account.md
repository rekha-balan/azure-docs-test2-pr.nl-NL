---
title: Connect an Amazon Web Services account to Azure Cost Management | Microsoft Docs
description: Connect an Amazon Web Services account to view cost and usage data in Cost Management reports.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/07/2018
ms.topic: conceptual
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: 119c7ba56056fdb10e910698ac9c9237977e697d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864379"
---
# <a name="connect-an-amazon-web-services-account"></a><span data-ttu-id="7ee85-103">Connect an Amazon Web Services account</span><span class="sxs-lookup"><span data-stu-id="7ee85-103">Connect an Amazon Web Services account</span></span>

<span data-ttu-id="7ee85-104">You have two options to connect your Amazon Web Services (AWS) account to Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-104">You have two options to connect your Amazon Web Services (AWS) account to Azure Cost Management.</span></span> <span data-ttu-id="7ee85-105">You can connect with an IAM role or with a read-only IAM user account.</span><span class="sxs-lookup"><span data-stu-id="7ee85-105">You can connect with an IAM role or with a read-only IAM user account.</span></span> <span data-ttu-id="7ee85-106">The IAM role is recommended because it allows you to delegate access with defined permissions to trusted entities.</span><span class="sxs-lookup"><span data-stu-id="7ee85-106">The IAM role is recommended because it allows you to delegate access with defined permissions to trusted entities.</span></span> <span data-ttu-id="7ee85-107">The IAM role doesn't require you to share long-term access keys.</span><span class="sxs-lookup"><span data-stu-id="7ee85-107">The IAM role doesn't require you to share long-term access keys.</span></span> <span data-ttu-id="7ee85-108">After you connect an AWS account to Cost Management, cost and usage data is available in Cost Management reports.</span><span class="sxs-lookup"><span data-stu-id="7ee85-108">After you connect an AWS account to Cost Management, cost and usage data is available in Cost Management reports.</span></span> <span data-ttu-id="7ee85-109">This document guides you through both options.</span><span class="sxs-lookup"><span data-stu-id="7ee85-109">This document guides you through both options.</span></span>

<span data-ttu-id="7ee85-110">For more information about AWS IAM identities, see [Identities (Users, Groups, and Roles)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html).</span><span class="sxs-lookup"><span data-stu-id="7ee85-110">For more information about AWS IAM identities, see [Identities (Users, Groups, and Roles)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html).</span></span>

<span data-ttu-id="7ee85-111">Also, you enable AWS detailed billing reports and store the information in an AWS simple storage service (S3) bucket.</span><span class="sxs-lookup"><span data-stu-id="7ee85-111">Also, you enable AWS detailed billing reports and store the information in an AWS simple storage service (S3) bucket.</span></span> <span data-ttu-id="7ee85-112">Detailed billing reports include billing charges with tag and resource information on an hourly basis.</span><span class="sxs-lookup"><span data-stu-id="7ee85-112">Detailed billing reports include billing charges with tag and resource information on an hourly basis.</span></span> <span data-ttu-id="7ee85-113">Storing the reports allows Cost Management to retrieve them from your bucket and display the information in its reports.</span><span class="sxs-lookup"><span data-stu-id="7ee85-113">Storing the reports allows Cost Management to retrieve them from your bucket and display the information in its reports.</span></span>


## <a name="aws-role-based-access"></a><span data-ttu-id="7ee85-114">AWS role-based access</span><span class="sxs-lookup"><span data-stu-id="7ee85-114">AWS role-based access</span></span>

<span data-ttu-id="7ee85-115">The following sections walk you through creating a read-only IAM role to provide access to Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-115">The following sections walk you through creating a read-only IAM role to provide access to Cost Management.</span></span>

### <a name="get-your-cost-management-account-external-id"></a><span data-ttu-id="7ee85-116">Get your Cost Management account external ID</span><span class="sxs-lookup"><span data-stu-id="7ee85-116">Get your Cost Management account external ID</span></span>

<span data-ttu-id="7ee85-117">The first step is to get the unique connection passphrase from the Azure Cost Management portal.</span><span class="sxs-lookup"><span data-stu-id="7ee85-117">The first step is to get the unique connection passphrase from the Azure Cost Management portal.</span></span> <span data-ttu-id="7ee85-118">It is used in AWS as the **External ID**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-118">It is used in AWS as the **External ID**.</span></span>

1. <span data-ttu-id="7ee85-119">Open the Cloudyn portal from the Azure portal or navigate to  [https://azure.cloudyn.com](https://azure.cloudyn.com) and sign in.</span><span class="sxs-lookup"><span data-stu-id="7ee85-119">Open the Cloudyn portal from the Azure portal or navigate to  [https://azure.cloudyn.com](https://azure.cloudyn.com) and sign in.</span></span>
2. <span data-ttu-id="7ee85-120">Click the cog symbol and then select **Cloud Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-120">Click the cog symbol and then select **Cloud Accounts**.</span></span>
3. <span data-ttu-id="7ee85-121">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-121">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span></span>
4. <span data-ttu-id="7ee85-122">In the **Add AWS Account** dialog, copy the **External ID** and save the value for AWS Role creation steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="7ee85-122">In the **Add AWS Account** dialog, copy the **External ID** and save the value for AWS Role creation steps in the next section.</span></span> <span data-ttu-id="7ee85-123">The External ID is unique to your account.</span><span class="sxs-lookup"><span data-stu-id="7ee85-123">The External ID is unique to your account.</span></span> <span data-ttu-id="7ee85-124">In the following image, the example External ID is _Contoso_ followed by a number.</span><span class="sxs-lookup"><span data-stu-id="7ee85-124">In the following image, the example External ID is _Contoso_ followed by a number.</span></span> <span data-ttu-id="7ee85-125">Your ID differs.</span><span class="sxs-lookup"><span data-stu-id="7ee85-125">Your ID differs.</span></span>  
    <span data-ttu-id="7ee85-126">![External ID](./media/connect-aws-account/external-id.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-126">![External ID](./media/connect-aws-account/external-id.png)</span></span>

### <a name="add-aws-read-only-role-based-access"></a><span data-ttu-id="7ee85-127">Add AWS read-only role-based access</span><span class="sxs-lookup"><span data-stu-id="7ee85-127">Add AWS read-only role-based access</span></span>

1. <span data-ttu-id="7ee85-128">Sign in to the AWS console at https://console.aws.amazon.com/iam/home and select **Roles**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-128">Sign in to the AWS console at https://console.aws.amazon.com/iam/home and select **Roles**.</span></span>
2. <span data-ttu-id="7ee85-129">Click **Create Role** and then select **Another AWS account**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-129">Click **Create Role** and then select **Another AWS account**.</span></span>
3. <span data-ttu-id="7ee85-130">In the **Account ID** box, paste `432263259397`.</span><span class="sxs-lookup"><span data-stu-id="7ee85-130">In the **Account ID** box, paste `432263259397`.</span></span> <span data-ttu-id="7ee85-131">This Account ID is the Cost Management data collector account assigned by AWS to the Cloudyn service.</span><span class="sxs-lookup"><span data-stu-id="7ee85-131">This Account ID is the Cost Management data collector account assigned by AWS to the Cloudyn service.</span></span> <span data-ttu-id="7ee85-132">Use the exact Account ID shown.</span><span class="sxs-lookup"><span data-stu-id="7ee85-132">Use the exact Account ID shown.</span></span>
4. <span data-ttu-id="7ee85-133">Next to **Options**, select **Require external ID**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-133">Next to **Options**, select **Require external ID**.</span></span> <span data-ttu-id="7ee85-134">Paste your unique value that copied previously from the **External ID** field in Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-134">Paste your unique value that copied previously from the **External ID** field in Cost Management.</span></span> <span data-ttu-id="7ee85-135">Then click **Next: Permissions**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-135">Then click **Next: Permissions**.</span></span>  
    <span data-ttu-id="7ee85-136">![Create role](./media/connect-aws-account/create-role01.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-136">![Create role](./media/connect-aws-account/create-role01.png)</span></span>
5. <span data-ttu-id="7ee85-137">Under **Attach permissions policies**, in the **Policy type** filter box search, type `ReadOnlyAccess`, select **ReadOnlyAccess**, then click **Next: Review**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-137">Under **Attach permissions policies**, in the **Policy type** filter box search, type `ReadOnlyAccess`, select **ReadOnlyAccess**, then click **Next: Review**.</span></span>  
    <span data-ttu-id="7ee85-138">![Read-only access](./media/connect-aws-account/readonlyaccess.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-138">![Read-only access](./media/connect-aws-account/readonlyaccess.png)</span></span>
6. <span data-ttu-id="7ee85-139">On the Review page, ensure your selections are correct and type a **Role name**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-139">On the Review page, ensure your selections are correct and type a **Role name**.</span></span> <span data-ttu-id="7ee85-140">For example, *Azure-Cost-Mgt*. Enter a **Role description**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-140">For example, *Azure-Cost-Mgt*. Enter a **Role description**.</span></span> <span data-ttu-id="7ee85-141">For example, _Role assignment for Azure Cost Management_, then click **Create role**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-141">For example, _Role assignment for Azure Cost Management_, then click **Create role**.</span></span>
7. <span data-ttu-id="7ee85-142">In the **Roles** list, click the role you created and copy the **Role ARN** value from the Summary page.</span><span class="sxs-lookup"><span data-stu-id="7ee85-142">In the **Roles** list, click the role you created and copy the **Role ARN** value from the Summary page.</span></span> <span data-ttu-id="7ee85-143">Use the Role ARN (Amazon Resource Name) value later when you register your configuration in Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-143">Use the Role ARN (Amazon Resource Name) value later when you register your configuration in Azure Cost Management.</span></span>  
    <span data-ttu-id="7ee85-144">![Role ARN](./media/connect-aws-account/role-arn.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-144">![Role ARN](./media/connect-aws-account/role-arn.png)</span></span>

### <a name="configure-aws-iam-role-access-in-cost-management"></a><span data-ttu-id="7ee85-145">Configure AWS IAM role access in Cost Management</span><span class="sxs-lookup"><span data-stu-id="7ee85-145">Configure AWS IAM role access in Cost Management</span></span>

1. <span data-ttu-id="7ee85-146">Open the Cloudyn portal from the Azure portal or navigate to  https://azure.cloudyn.com/ and sign in.</span><span class="sxs-lookup"><span data-stu-id="7ee85-146">Open the Cloudyn portal from the Azure portal or navigate to  https://azure.cloudyn.com/ and sign in.</span></span>
2. <span data-ttu-id="7ee85-147">Click the cog symbol and then select **Cloud Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-147">Click the cog symbol and then select **Cloud Accounts**.</span></span>
3. <span data-ttu-id="7ee85-148">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-148">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span></span>
4. <span data-ttu-id="7ee85-149">In **Account Name**, type a name for the account.</span><span class="sxs-lookup"><span data-stu-id="7ee85-149">In **Account Name**, type a name for the account.</span></span>
5. <span data-ttu-id="7ee85-150">Next to **Access Type**, select **IAM Role**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-150">Next to **Access Type**, select **IAM Role**.</span></span>
6. <span data-ttu-id="7ee85-151">In the **Role ARN** field, paste the value you previously copied and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-151">In the **Role ARN** field, paste the value you previously copied and then click **Save**.</span></span>  
    <span data-ttu-id="7ee85-152">![Add AWS Account box](./media/connect-aws-account/add-aws-account-box.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-152">![Add AWS Account box](./media/connect-aws-account/add-aws-account-box.png)</span></span>


<span data-ttu-id="7ee85-153">Your AWS account appears in the list of accounts.</span><span class="sxs-lookup"><span data-stu-id="7ee85-153">Your AWS account appears in the list of accounts.</span></span> <span data-ttu-id="7ee85-154">The **Owner ID** listed matches your Role ARN value.</span><span class="sxs-lookup"><span data-stu-id="7ee85-154">The **Owner ID** listed matches your Role ARN value.</span></span> <span data-ttu-id="7ee85-155">Your **Account Status** should have a green check mark symbol indicating that Cost Management can access your AWS account.</span><span class="sxs-lookup"><span data-stu-id="7ee85-155">Your **Account Status** should have a green check mark symbol indicating that Cost Management can access your AWS account.</span></span> <span data-ttu-id="7ee85-156">Until you enable detailed AWS billing, your consolidation status appears as **Standalone**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-156">Until you enable detailed AWS billing, your consolidation status appears as **Standalone**.</span></span>

![AWS account status](./media/connect-aws-account/aws-account-status01.png)

<span data-ttu-id="7ee85-158">Cost Management starts collecting the data and populating reports.</span><span class="sxs-lookup"><span data-stu-id="7ee85-158">Cost Management starts collecting the data and populating reports.</span></span> <span data-ttu-id="7ee85-159">Next, [enable detailed AWS billing](#enable-detailed-aws-billing).</span><span class="sxs-lookup"><span data-stu-id="7ee85-159">Next, [enable detailed AWS billing](#enable-detailed-aws-billing).</span></span>


## <a name="aws-user-based-access"></a><span data-ttu-id="7ee85-160">AWS user-based access</span><span class="sxs-lookup"><span data-stu-id="7ee85-160">AWS user-based access</span></span>

<span data-ttu-id="7ee85-161">The following sections walk you through creating a read-only user to provide access to Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-161">The following sections walk you through creating a read-only user to provide access to Cost Management.</span></span>

### <a name="add-aws-read-only-user-based-access"></a><span data-ttu-id="7ee85-162">Add AWS read-only user-based access</span><span class="sxs-lookup"><span data-stu-id="7ee85-162">Add AWS read-only user-based access</span></span>

1. <span data-ttu-id="7ee85-163">Sign in to the AWS console at https://console.aws.amazon.com/iam/home and select **Users**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-163">Sign in to the AWS console at https://console.aws.amazon.com/iam/home and select **Users**.</span></span>
2. <span data-ttu-id="7ee85-164">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-164">Click **Add User**.</span></span>
3. <span data-ttu-id="7ee85-165">In the **User name** field, type a user name.</span><span class="sxs-lookup"><span data-stu-id="7ee85-165">In the **User name** field, type a user name.</span></span>
4. <span data-ttu-id="7ee85-166">For **Access type**, select **Programmatic access** and click **Next: Permissions**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-166">For **Access type**, select **Programmatic access** and click **Next: Permissions**.</span></span>  
    <span data-ttu-id="7ee85-167">![Add user](./media/connect-aws-account/add-user01.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-167">![Add user](./media/connect-aws-account/add-user01.png)</span></span>
5. <span data-ttu-id="7ee85-168">For permissions, select **Attach existing policies directly**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-168">For permissions, select **Attach existing policies directly**.</span></span>
6. <span data-ttu-id="7ee85-169">Under **Attach permissions policies**, in the **Policy type** filter box search, type `ReadOnlyAccess`, select **ReadOnlyAccess**, and then click **Next: Review**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-169">Under **Attach permissions policies**, in the **Policy type** filter box search, type `ReadOnlyAccess`, select **ReadOnlyAccess**, and then click **Next: Review**.</span></span>  
    <span data-ttu-id="7ee85-170">![Set permissions for user](./media/connect-aws-account/set-permission-for-user.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-170">![Set permissions for user](./media/connect-aws-account/set-permission-for-user.png)</span></span>
7. <span data-ttu-id="7ee85-171">On the Review page, ensure your selections are correct then click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-171">On the Review page, ensure your selections are correct then click **Create user**.</span></span>
8. <span data-ttu-id="7ee85-172">On the Complete page, your Access key ID and Secret access key are shown.</span><span class="sxs-lookup"><span data-stu-id="7ee85-172">On the Complete page, your Access key ID and Secret access key are shown.</span></span> <span data-ttu-id="7ee85-173">You use this information to configure registration in Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-173">You use this information to configure registration in Cost Management.</span></span>
9. <span data-ttu-id="7ee85-174">Click **Download .csv** and save the credentials.csv file to a secure location.</span><span class="sxs-lookup"><span data-stu-id="7ee85-174">Click **Download .csv** and save the credentials.csv file to a secure location.</span></span>  
    <span data-ttu-id="7ee85-175">![Download credentials](./media/connect-aws-account/download-csv.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-175">![Download credentials](./media/connect-aws-account/download-csv.png)</span></span>

### <a name="configure-aws-iam-user-based-access-in-cost-management"></a><span data-ttu-id="7ee85-176">Configure AWS IAM user-based access in Cost Management</span><span class="sxs-lookup"><span data-stu-id="7ee85-176">Configure AWS IAM user-based access in Cost Management</span></span>

1. <span data-ttu-id="7ee85-177">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com/ and sign in.</span><span class="sxs-lookup"><span data-stu-id="7ee85-177">Open the Cloudyn portal from the Azure portal or navigate to https://azure.cloudyn.com/ and sign in.</span></span>
2. <span data-ttu-id="7ee85-178">Click the cog symbol and then select **Cloud Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-178">Click the cog symbol and then select **Cloud Accounts**.</span></span>
3. <span data-ttu-id="7ee85-179">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-179">In Accounts Management, select the **AWS Accounts** tab and then click **Add new +**.</span></span>
4. <span data-ttu-id="7ee85-180">For **Account Name**, type an account name.</span><span class="sxs-lookup"><span data-stu-id="7ee85-180">For **Account Name**, type an account name.</span></span>
5. <span data-ttu-id="7ee85-181">Next to **Access Type**, select **IAM User**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-181">Next to **Access Type**, select **IAM User**.</span></span>
6. <span data-ttu-id="7ee85-182">In **Access Key**, paste the **Access key ID** value from the credentials.csv file.</span><span class="sxs-lookup"><span data-stu-id="7ee85-182">In **Access Key**, paste the **Access key ID** value from the credentials.csv file.</span></span>
7. <span data-ttu-id="7ee85-183">In **Secret Key**, paste the **Secret access key** value from the credentials.csv file and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-183">In **Secret Key**, paste the **Secret access key** value from the credentials.csv file and then click **Save**.</span></span>  

<span data-ttu-id="7ee85-184">Your AWS account appears in the list of accounts.</span><span class="sxs-lookup"><span data-stu-id="7ee85-184">Your AWS account appears in the list of accounts.</span></span> <span data-ttu-id="7ee85-185">Your **Account Status** should have a green check mark symbol.</span><span class="sxs-lookup"><span data-stu-id="7ee85-185">Your **Account Status** should have a green check mark symbol.</span></span>

<span data-ttu-id="7ee85-186">Cost Management starts collecting the data and populating reports.</span><span class="sxs-lookup"><span data-stu-id="7ee85-186">Cost Management starts collecting the data and populating reports.</span></span> <span data-ttu-id="7ee85-187">Next, [enable detailed AWS billing](#enable-detailed-aws-billing).</span><span class="sxs-lookup"><span data-stu-id="7ee85-187">Next, [enable detailed AWS billing](#enable-detailed-aws-billing).</span></span>

## <a name="enable-detailed-aws-billing"></a><span data-ttu-id="7ee85-188">Enable detailed AWS billing</span><span class="sxs-lookup"><span data-stu-id="7ee85-188">Enable detailed AWS billing</span></span>

<span data-ttu-id="7ee85-189">Use the following steps to get your AWS Role ARN.</span><span class="sxs-lookup"><span data-stu-id="7ee85-189">Use the following steps to get your AWS Role ARN.</span></span> <span data-ttu-id="7ee85-190">You use the Role ARN to grant read permissions to a billing bucket.</span><span class="sxs-lookup"><span data-stu-id="7ee85-190">You use the Role ARN to grant read permissions to a billing bucket.</span></span>

1. <span data-ttu-id="7ee85-191">Sign in to the AWS console at https://console.aws.amazon.com and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-191">Sign in to the AWS console at https://console.aws.amazon.com and select **Services**.</span></span>
2. <span data-ttu-id="7ee85-192">In the Service Search box type *IAM*, and select that option.</span><span class="sxs-lookup"><span data-stu-id="7ee85-192">In the Service Search box type *IAM*, and select that option.</span></span>
3. <span data-ttu-id="7ee85-193">Select **Roles** from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="7ee85-193">Select **Roles** from the left-hand menu.</span></span>
4. <span data-ttu-id="7ee85-194">In the list of Roles, select the role that you created for Cloudyn access.</span><span class="sxs-lookup"><span data-stu-id="7ee85-194">In the list of Roles, select the role that you created for Cloudyn access.</span></span>
5. <span data-ttu-id="7ee85-195">On the Roles Summary page, click to copy the **Role ARN**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-195">On the Roles Summary page, click to copy the **Role ARN**.</span></span> <span data-ttu-id="7ee85-196">Keep the Role ARN handy for later steps.</span><span class="sxs-lookup"><span data-stu-id="7ee85-196">Keep the Role ARN handy for later steps.</span></span>

### <a name="create-an-s3-bucket"></a><span data-ttu-id="7ee85-197">Create an S3 bucket</span><span class="sxs-lookup"><span data-stu-id="7ee85-197">Create an S3 bucket</span></span>

<span data-ttu-id="7ee85-198">You create an S3 bucket to store detailed billing information.</span><span class="sxs-lookup"><span data-stu-id="7ee85-198">You create an S3 bucket to store detailed billing information.</span></span>

1. <span data-ttu-id="7ee85-199">Sign in to the AWS console at https://console.aws.amazon.com and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-199">Sign in to the AWS console at https://console.aws.amazon.com and select **Services**.</span></span>
2. <span data-ttu-id="7ee85-200">In the Service Search box type *S3*, and select **S3**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-200">In the Service Search box type *S3*, and select **S3**.</span></span>
3. <span data-ttu-id="7ee85-201">On the Amazon S3 page, click **Create bucket**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-201">On the Amazon S3 page, click **Create bucket**.</span></span>
4. <span data-ttu-id="7ee85-202">In the Create bucket wizard, choose a Bucket name and Region and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-202">In the Create bucket wizard, choose a Bucket name and Region and then click **Next**.</span></span>  
    <span data-ttu-id="7ee85-203">![Create bucket](./media/connect-aws-account/create-bucket.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-203">![Create bucket](./media/connect-aws-account/create-bucket.png)</span></span>
5. <span data-ttu-id="7ee85-204">On the **Set properties** page, keep the default values, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-204">On the **Set properties** page, keep the default values, and then click **Next**.</span></span>
6. <span data-ttu-id="7ee85-205">On the Review page, click **Create bucket**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-205">On the Review page, click **Create bucket**.</span></span> <span data-ttu-id="7ee85-206">Your bucket list is displayed.</span><span class="sxs-lookup"><span data-stu-id="7ee85-206">Your bucket list is displayed.</span></span>
7. <span data-ttu-id="7ee85-207">Click the bucket that you created and select the **Permissions** tab and then select **Bucket Policy**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-207">Click the bucket that you created and select the **Permissions** tab and then select **Bucket Policy**.</span></span> <span data-ttu-id="7ee85-208">The Bucket policy editor opens.</span><span class="sxs-lookup"><span data-stu-id="7ee85-208">The Bucket policy editor opens.</span></span>
8. <span data-ttu-id="7ee85-209">Copy the following JSON example and paste it in the Bucket policy editor.</span><span class="sxs-lookup"><span data-stu-id="7ee85-209">Copy the following JSON example and paste it in the Bucket policy editor.</span></span>
  - <span data-ttu-id="7ee85-210">Replace `<BillingBucketName>` with the name of your S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="7ee85-210">Replace `<BillingBucketName>` with the name of your S3 bucket.</span></span>
  - <span data-ttu-id="7ee85-211">Replace `<ReadOnlyUserOrRole>` with the Role or User ARN that you had previously copied.</span><span class="sxs-lookup"><span data-stu-id="7ee85-211">Replace `<ReadOnlyUserOrRole>` with the Role or User ARN that you had previously copied.</span></span>

  ```
  {
    "Version": "2012-10-17",
    "Id": "Policy1426774604000",
    "Statement": [
        {
            "Sid": "Stmt1426774604000",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::386209384616:root"
            },
            "Action": [
                "s3:GetBucketAcl",
                "s3:GetBucketPolicy"
            ],
            "Resource": "arn:aws:s3:::<BillingBucketName>"
        },
        {
            "Sid": "Stmt1426774604001",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::386209384616:root"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<BillingBucketName>/*"
        },
        {
            "Sid": "Stmt1426774604002",
            "Effect": "Allow",
            "Principal": {
                "AWS": "<ReadOnlyUserOrRole>"
            },
            "Action": [
                "s3:List*",
                "s3:Get*"
            ],
            "Resource": "arn:aws:s3:::<BillingBucketName>/*"
        }
    ]
  }
  ```

9. <span data-ttu-id="7ee85-212">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-212">Click **Save**.</span></span>  
    <span data-ttu-id="7ee85-213">![Bucket policy editor](./media/connect-aws-account/bucket-policy-editor.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-213">![Bucket policy editor](./media/connect-aws-account/bucket-policy-editor.png)</span></span>


### <a name="enable-aws-billing-reports"></a><span data-ttu-id="7ee85-214">Enable AWS billing reports</span><span class="sxs-lookup"><span data-stu-id="7ee85-214">Enable AWS billing reports</span></span>

<span data-ttu-id="7ee85-215">After you create and configure the S3 bucket, navigate to [Billing Preferences](https://console.aws.amazon.com/billing/home?#/preference) in the AWS console.</span><span class="sxs-lookup"><span data-stu-id="7ee85-215">After you create and configure the S3 bucket, navigate to [Billing Preferences](https://console.aws.amazon.com/billing/home?#/preference) in the AWS console.</span></span>

1. <span data-ttu-id="7ee85-216">On the Preferences page, select **Receive Billing Reports**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-216">On the Preferences page, select **Receive Billing Reports**.</span></span>
2. <span data-ttu-id="7ee85-217">Under **Receive Billing Reports**, enter the name of the bucket that you created and then click **Verify**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-217">Under **Receive Billing Reports**, enter the name of the bucket that you created and then click **Verify**.</span></span>  
3. <span data-ttu-id="7ee85-218">Select all four report granularity options and then click **Save preferences**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-218">Select all four report granularity options and then click **Save preferences**.</span></span>  
    <span data-ttu-id="7ee85-219">![Enable reports](./media/connect-aws-account/enable-reports.png)</span><span class="sxs-lookup"><span data-stu-id="7ee85-219">![Enable reports](./media/connect-aws-account/enable-reports.png)</span></span>

<span data-ttu-id="7ee85-220">Cost Management retrieves detailed billing information from your S3 bucket and populates reports after detailed billing is enabled.</span><span class="sxs-lookup"><span data-stu-id="7ee85-220">Cost Management retrieves detailed billing information from your S3 bucket and populates reports after detailed billing is enabled.</span></span> <span data-ttu-id="7ee85-221">It can take up to 24 hours until detailed billing data appears in the Cloudyn console.</span><span class="sxs-lookup"><span data-stu-id="7ee85-221">It can take up to 24 hours until detailed billing data appears in the Cloudyn console.</span></span> <span data-ttu-id="7ee85-222">When detailed billing data is available, your account consolidation status appears as **Consolidated**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-222">When detailed billing data is available, your account consolidation status appears as **Consolidated**.</span></span> <span data-ttu-id="7ee85-223">Account status appears as **Completed**.</span><span class="sxs-lookup"><span data-stu-id="7ee85-223">Account status appears as **Completed**.</span></span>

![Account Consolidated Status](./media/connect-aws-account/consolidated-status.png)

<span data-ttu-id="7ee85-225">Some of the optimization reports may require a few days of data to get an adequate data sample size for accurate recommendations.</span><span class="sxs-lookup"><span data-stu-id="7ee85-225">Some of the optimization reports may require a few days of data to get an adequate data sample size for accurate recommendations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ee85-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ee85-226">Next steps</span></span>

- <span data-ttu-id="7ee85-227">To learn more about Azure Cost Management, continue to the [Review usage and costs](tutorial-review-usage.md) tutorial for Cost Management.</span><span class="sxs-lookup"><span data-stu-id="7ee85-227">To learn more about Azure Cost Management, continue to the [Review usage and costs](tutorial-review-usage.md) tutorial for Cost Management.</span></span>
