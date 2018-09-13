# <a name="compute"></a><span data-ttu-id="7af3b-101">Compute</span><span class="sxs-lookup"><span data-stu-id="7af3b-101">Compute</span></span>
<span data-ttu-id="7af3b-102">Azure enables you to deploy and monitor your application code running inside a Microsoft data center.</span><span class="sxs-lookup"><span data-stu-id="7af3b-102">Azure enables you to deploy and monitor your application code running inside a Microsoft data center.</span></span> <span data-ttu-id="7af3b-103">When you create an application and run it on Azure, the code and configuration together is called an Azure hosted service.</span><span class="sxs-lookup"><span data-stu-id="7af3b-103">When you create an application and run it on Azure, the code and configuration together is called an Azure hosted service.</span></span> <span data-ttu-id="7af3b-104">Hosted services are easy to manage, scale up and down, reconfigure, and update with new versions of your application's code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-104">Hosted services are easy to manage, scale up and down, reconfigure, and update with new versions of your application's code.</span></span> <span data-ttu-id="7af3b-105">This article focuses on the Azure hosted service application model.<a id="compare" name="compare"></a></span><span class="sxs-lookup"><span data-stu-id="7af3b-105">This article focuses on the Azure hosted service application model.<a id="compare" name="compare"></a></span></span>

## <span data-ttu-id="7af3b-106">Table of Contents<a id="_GoBack" name="_GoBack"></a></span><span class="sxs-lookup"><span data-stu-id="7af3b-106">Table of Contents<a id="_GoBack" name="_GoBack"></a></span></span>
* <span data-ttu-id="7af3b-107">[Azure Application Model Benefits][Azure Application Model Benefits]</span><span class="sxs-lookup"><span data-stu-id="7af3b-107">[Azure Application Model Benefits][Azure Application Model Benefits]</span></span>
* <span data-ttu-id="7af3b-108">[Hosted Service Core Concepts][Hosted Service Core Concepts]</span><span class="sxs-lookup"><span data-stu-id="7af3b-108">[Hosted Service Core Concepts][Hosted Service Core Concepts]</span></span>
* <span data-ttu-id="7af3b-109">[Hosted Service Design Considerations][Hosted Service Design Considerations]</span><span class="sxs-lookup"><span data-stu-id="7af3b-109">[Hosted Service Design Considerations][Hosted Service Design Considerations]</span></span>
* <span data-ttu-id="7af3b-110">[Designing your Application for Scale][Designing your Application for Scale]</span><span class="sxs-lookup"><span data-stu-id="7af3b-110">[Designing your Application for Scale][Designing your Application for Scale]</span></span>
* <span data-ttu-id="7af3b-111">[Hosted Service Definition and Configuration][Hosted Service Definition and Configuration]</span><span class="sxs-lookup"><span data-stu-id="7af3b-111">[Hosted Service Definition and Configuration][Hosted Service Definition and Configuration]</span></span>
* <span data-ttu-id="7af3b-112">[The Service Definition File][The Service Definition File]</span><span class="sxs-lookup"><span data-stu-id="7af3b-112">[The Service Definition File][The Service Definition File]</span></span>
* <span data-ttu-id="7af3b-113">[The Service Configuration File][The Service Configuration File]</span><span class="sxs-lookup"><span data-stu-id="7af3b-113">[The Service Configuration File][The Service Configuration File]</span></span>
* <span data-ttu-id="7af3b-114">[Creating and Deploying a Hosted Service][Creating and Deploying a Hosted Service]</span><span class="sxs-lookup"><span data-stu-id="7af3b-114">[Creating and Deploying a Hosted Service][Creating and Deploying a Hosted Service]</span></span>
* <span data-ttu-id="7af3b-115">[References][References]</span><span class="sxs-lookup"><span data-stu-id="7af3b-115">[References][References]</span></span>

## <span data-ttu-id="7af3b-116"><a id="benefits"> </a>Azure Application Model Benefits</span><span class="sxs-lookup"><span data-stu-id="7af3b-116"><a id="benefits"> </a>Azure Application Model Benefits</span></span>
<span data-ttu-id="7af3b-117">When you deploy your application as a hosted service, Azure creates one or more virtual machines (VMs) that contain your application's code, and boots the VMs on physical machines residing in one of the Azure data centers.</span><span class="sxs-lookup"><span data-stu-id="7af3b-117">When you deploy your application as a hosted service, Azure creates one or more virtual machines (VMs) that contain your application's code, and boots the VMs on physical machines residing in one of the Azure data centers.</span></span> <span data-ttu-id="7af3b-118">As client requests to your hosted application enter the data center, a load balancer distributes these requests equally to the VMs.</span><span class="sxs-lookup"><span data-stu-id="7af3b-118">As client requests to your hosted application enter the data center, a load balancer distributes these requests equally to the VMs.</span></span> <span data-ttu-id="7af3b-119">While your application is hosted in Azure, it gets three key benefits:</span><span class="sxs-lookup"><span data-stu-id="7af3b-119">While your application is hosted in Azure, it gets three key benefits:</span></span>

* <span data-ttu-id="7af3b-120">**High availability.**</span><span class="sxs-lookup"><span data-stu-id="7af3b-120">**High availability.**</span></span> <span data-ttu-id="7af3b-121">High availability means Azure ensures that your application is running as much as possible and is able to respond to client requests.</span><span class="sxs-lookup"><span data-stu-id="7af3b-121">High availability means Azure ensures that your application is running as much as possible and is able to respond to client requests.</span></span> <span data-ttu-id="7af3b-122">If your application terminates (due to an unhandled exception, for example), then Azure will detect this, and it will automatically re-start your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-122">If your application terminates (due to an unhandled exception, for example), then Azure will detect this, and it will automatically re-start your application.</span></span> <span data-ttu-id="7af3b-123">If the machine your application is running on experiences some kind of hardware failure, then Azure will also detect this and automatically create a new VM on another working physical machine and run your code from there.</span><span class="sxs-lookup"><span data-stu-id="7af3b-123">If the machine your application is running on experiences some kind of hardware failure, then Azure will also detect this and automatically create a new VM on another working physical machine and run your code from there.</span></span> <span data-ttu-id="7af3b-124">NOTE: In order for your application to get Microsoft's Service Level Agreement of 99.95% available, you must have at least two VMs running your application code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-124">NOTE: In order for your application to get Microsoft's Service Level Agreement of 99.95% available, you must have at least two VMs running your application code.</span></span> <span data-ttu-id="7af3b-125">This allows one VM to process client requests while Azure moves your code from a failed VM to a new, good VM.</span><span class="sxs-lookup"><span data-stu-id="7af3b-125">This allows one VM to process client requests while Azure moves your code from a failed VM to a new, good VM.</span></span>
* <span data-ttu-id="7af3b-126">**Scalability.**</span><span class="sxs-lookup"><span data-stu-id="7af3b-126">**Scalability.**</span></span> <span data-ttu-id="7af3b-127">Azure lets you easily and dynamically change the number of VMs running your application code to handle the actual load being placed on your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-127">Azure lets you easily and dynamically change the number of VMs running your application code to handle the actual load being placed on your application.</span></span> <span data-ttu-id="7af3b-128">This allows you to adjust your application to the workload that your customers are placing on it while paying only for the VMs you need when you need them.</span><span class="sxs-lookup"><span data-stu-id="7af3b-128">This allows you to adjust your application to the workload that your customers are placing on it while paying only for the VMs you need when you need them.</span></span> <span data-ttu-id="7af3b-129">When you want to change the number of VMs, Azure responds within minutes making it possible to dynamically change the number of VMs running as often as desired.</span><span class="sxs-lookup"><span data-stu-id="7af3b-129">When you want to change the number of VMs, Azure responds within minutes making it possible to dynamically change the number of VMs running as often as desired.</span></span>
* <span data-ttu-id="7af3b-130">**Manageability.**</span><span class="sxs-lookup"><span data-stu-id="7af3b-130">**Manageability.**</span></span> <span data-ttu-id="7af3b-131">Because Azure is a Platform as a Service (PaaS) offering, it manages the infrastructure (the hardware itself, electricity, and networking) required to keep these machines running.</span><span class="sxs-lookup"><span data-stu-id="7af3b-131">Because Azure is a Platform as a Service (PaaS) offering, it manages the infrastructure (the hardware itself, electricity, and networking) required to keep these machines running.</span></span> <span data-ttu-id="7af3b-132">Azure also manages the platform, ensuring an up-to-date operating system with all the correct patches and security updates, as well as component updates such as the .NET Framework and Internet Information Server.</span><span class="sxs-lookup"><span data-stu-id="7af3b-132">Azure also manages the platform, ensuring an up-to-date operating system with all the correct patches and security updates, as well as component updates such as the .NET Framework and Internet Information Server.</span></span> <span data-ttu-id="7af3b-133">Because all the VMs are running Windows Server 2008, Azure provides additional features such as diagnostic monitoring, remote desktop support, firewalls, and certificate store configuration.</span><span class="sxs-lookup"><span data-stu-id="7af3b-133">Because all the VMs are running Windows Server 2008, Azure provides additional features such as diagnostic monitoring, remote desktop support, firewalls, and certificate store configuration.</span></span> <span data-ttu-id="7af3b-134">All these features are provided at no extra cost.</span><span class="sxs-lookup"><span data-stu-id="7af3b-134">All these features are provided at no extra cost.</span></span> <span data-ttu-id="7af3b-135">In fact, when you run your application in Azure, the Windows Server 2008 operating system (OS) license is included.</span><span class="sxs-lookup"><span data-stu-id="7af3b-135">In fact, when you run your application in Azure, the Windows Server 2008 operating system (OS) license is included.</span></span> <span data-ttu-id="7af3b-136">Since all of the VMs are running Windows Server 2008, any code that runs on Windows Server 2008 works just fine when running in Azure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-136">Since all of the VMs are running Windows Server 2008, any code that runs on Windows Server 2008 works just fine when running in Azure.</span></span>

## <span data-ttu-id="7af3b-137"><a id="concepts"> </a>Hosted Service Core Concepts</span><span class="sxs-lookup"><span data-stu-id="7af3b-137"><a id="concepts"> </a>Hosted Service Core Concepts</span></span>
<span data-ttu-id="7af3b-138">When your application is deployed as a hosted service in Azure, it runs as one or more *roles.*</span><span class="sxs-lookup"><span data-stu-id="7af3b-138">When your application is deployed as a hosted service in Azure, it runs as one or more *roles.*</span></span> <span data-ttu-id="7af3b-139">A *role* simply refers to application files and configuration.</span><span class="sxs-lookup"><span data-stu-id="7af3b-139">A *role* simply refers to application files and configuration.</span></span> <span data-ttu-id="7af3b-140">You can define one or more roles for your application, each with its own set of application files and configuration.</span><span class="sxs-lookup"><span data-stu-id="7af3b-140">You can define one or more roles for your application, each with its own set of application files and configuration.</span></span> <span data-ttu-id="7af3b-141">For each role in your application, you can specify the number of VMs, or *role instances*, to run.</span><span class="sxs-lookup"><span data-stu-id="7af3b-141">For each role in your application, you can specify the number of VMs, or *role instances*, to run.</span></span> <span data-ttu-id="7af3b-142">The figure below show two simple examples of an application modeled as a hosted service using roles and role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-142">The figure below show two simple examples of an application modeled as a hosted service using roles and role instances.</span></span>

##### <a name="figure-1-a-single-role-with-three-instances-vms-running-in-an-azure-data-center"></a><span data-ttu-id="7af3b-143">Figure 1: A single role with three instances (VMs) running in an Azure data center</span><span class="sxs-lookup"><span data-stu-id="7af3b-143">Figure 1: A single role with three instances (VMs) running in an Azure data center</span></span>
![image][0]

##### <a name="figure-2-two-roles-each-with-two-instances-vms-running-in-an-azure-data-center"></a><span data-ttu-id="7af3b-145">Figure 2: Two roles, each with two instances (VMs), running in an Azure data center</span><span class="sxs-lookup"><span data-stu-id="7af3b-145">Figure 2: Two roles, each with two instances (VMs), running in an Azure data center</span></span>
![image][1]

<span data-ttu-id="7af3b-147">Role instances typically process Internet client requests entering the data center through what is called an *input endpoint*.</span><span class="sxs-lookup"><span data-stu-id="7af3b-147">Role instances typically process Internet client requests entering the data center through what is called an *input endpoint*.</span></span> <span data-ttu-id="7af3b-148">A single role can have 0 or more input endpoints.</span><span class="sxs-lookup"><span data-stu-id="7af3b-148">A single role can have 0 or more input endpoints.</span></span> <span data-ttu-id="7af3b-149">Each endpoint indicates a protocol (HTTP, HTTPS, or TCP) and a port.</span><span class="sxs-lookup"><span data-stu-id="7af3b-149">Each endpoint indicates a protocol (HTTP, HTTPS, or TCP) and a port.</span></span> <span data-ttu-id="7af3b-150">It is common to configure a role to have two input endpoints: HTTP listening on port 80 and HTTPS listening on port 443.</span><span class="sxs-lookup"><span data-stu-id="7af3b-150">It is common to configure a role to have two input endpoints: HTTP listening on port 80 and HTTPS listening on port 443.</span></span> <span data-ttu-id="7af3b-151">The figure below shows an example of two different roles with different input endpoints directing client requests to them.</span><span class="sxs-lookup"><span data-stu-id="7af3b-151">The figure below shows an example of two different roles with different input endpoints directing client requests to them.</span></span>

![image][2]

<span data-ttu-id="7af3b-153">When you create a hosted service in Azure, it is assigned a publicly addressable IP address that clients can use to access it.</span><span class="sxs-lookup"><span data-stu-id="7af3b-153">When you create a hosted service in Azure, it is assigned a publicly addressable IP address that clients can use to access it.</span></span> <span data-ttu-id="7af3b-154">Upon creating the hosted service you must also select a URL prefix that is mapped to that IP address.</span><span class="sxs-lookup"><span data-stu-id="7af3b-154">Upon creating the hosted service you must also select a URL prefix that is mapped to that IP address.</span></span> <span data-ttu-id="7af3b-155">This prefix must be unique as you are essentially reserving the *prefix*.cloudapp.net URL so that no one else can have it.</span><span class="sxs-lookup"><span data-stu-id="7af3b-155">This prefix must be unique as you are essentially reserving the *prefix*.cloudapp.net URL so that no one else can have it.</span></span> <span data-ttu-id="7af3b-156">Clients communicate with your role instances by using the URL.</span><span class="sxs-lookup"><span data-stu-id="7af3b-156">Clients communicate with your role instances by using the URL.</span></span> <span data-ttu-id="7af3b-157">Usually, you will not distribute or publish the Azure *prefix*.cloudapp.net URL.</span><span class="sxs-lookup"><span data-stu-id="7af3b-157">Usually, you will not distribute or publish the Azure *prefix*.cloudapp.net URL.</span></span> <span data-ttu-id="7af3b-158">Instead, you will purchase a DNS name from your DNS registrar of choice and configure your DNS name to redirect client requests to the Azure URL.</span><span class="sxs-lookup"><span data-stu-id="7af3b-158">Instead, you will purchase a DNS name from your DNS registrar of choice and configure your DNS name to redirect client requests to the Azure URL.</span></span> <span data-ttu-id="7af3b-159">For more details, see [Configuring a Custom Domain Name in Azure][Configuring a Custom Domain Name in Azure].</span><span class="sxs-lookup"><span data-stu-id="7af3b-159">For more details, see [Configuring a Custom Domain Name in Azure][Configuring a Custom Domain Name in Azure].</span></span>

## <span data-ttu-id="7af3b-160"><a id="considerations"> </a>Hosted Service Design Considerations</span><span class="sxs-lookup"><span data-stu-id="7af3b-160"><a id="considerations"> </a>Hosted Service Design Considerations</span></span>
<span data-ttu-id="7af3b-161">When designing an application to run in a cloud environment, there are several considerations to think about such as latency, high-availability, and scalability.</span><span class="sxs-lookup"><span data-stu-id="7af3b-161">When designing an application to run in a cloud environment, there are several considerations to think about such as latency, high-availability, and scalability.</span></span>

<span data-ttu-id="7af3b-162">Deciding where to locate your application code is an important consideration when running a hosted service in Azure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-162">Deciding where to locate your application code is an important consideration when running a hosted service in Azure.</span></span> <span data-ttu-id="7af3b-163">It is common to deploy your application to data centers that are closest to your clients to reduce latency and get the best performance possible.</span><span class="sxs-lookup"><span data-stu-id="7af3b-163">It is common to deploy your application to data centers that are closest to your clients to reduce latency and get the best performance possible.</span></span>
<span data-ttu-id="7af3b-164">However, you might choose a data center closer to your company or closer to your data if you have some jurisdictional or legal concerns about your data and where it resides.</span><span class="sxs-lookup"><span data-stu-id="7af3b-164">However, you might choose a data center closer to your company or closer to your data if you have some jurisdictional or legal concerns about your data and where it resides.</span></span> <span data-ttu-id="7af3b-165">There are six data centers around the globe capable of hosting your application code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-165">There are six data centers around the globe capable of hosting your application code.</span></span> <span data-ttu-id="7af3b-166">The table below shows the available locations:</span><span class="sxs-lookup"><span data-stu-id="7af3b-166">The table below shows the available locations:</span></span>

<table border="2" cellspacing="0" cellpadding="5" style="border: 2px solid #000000;">

<tbody>

<tr>

<td style="width: 100px;"><span data-ttu-id="7af3b-167">
\*\*Country/Region**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-167">
\*\*Country/Region**

</span></span></td>

<td style="width: 200px;"><span data-ttu-id="7af3b-168">
\*\*Sub-regions**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-168">
\*\*Sub-regions**

</span></span></td>
</tr>

<tr>

<td>
<span data-ttu-id="7af3b-169">United States</span><span class="sxs-lookup"><span data-stu-id="7af3b-169">United States</span></span>

</td>

<td>
<span data-ttu-id="7af3b-170">South Central & North Central</span><span class="sxs-lookup"><span data-stu-id="7af3b-170">South Central & North Central</span></span>

</td>
</tr>

<tr>

<td>
<span data-ttu-id="7af3b-171">Europe</span><span class="sxs-lookup"><span data-stu-id="7af3b-171">Europe</span></span>

</td>

<td>
<span data-ttu-id="7af3b-172">North & West</span><span class="sxs-lookup"><span data-stu-id="7af3b-172">North & West</span></span>

</td>
</tr>

<tr>

<td>
<span data-ttu-id="7af3b-173">Asia</span><span class="sxs-lookup"><span data-stu-id="7af3b-173">Asia</span></span>

</td>

<td>
<span data-ttu-id="7af3b-174">Southeast & East</span><span class="sxs-lookup"><span data-stu-id="7af3b-174">Southeast & East</span></span>

</td>
</tr>
</tbody>
</table>
<span data-ttu-id="7af3b-175">When creating a hosted service, you select a sub-region indicating the location in which you want your code to execute.</span><span class="sxs-lookup"><span data-stu-id="7af3b-175">When creating a hosted service, you select a sub-region indicating the location in which you want your code to execute.</span></span>

<span data-ttu-id="7af3b-176">To achieve high availability and scalability, it is critically important that your application's data be kept in a central repository accessible to multiple role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-176">To achieve high availability and scalability, it is critically important that your application's data be kept in a central repository accessible to multiple role instances.</span></span> <span data-ttu-id="7af3b-177">To help with this, Azure offers several storage options such as blobs, tables, and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7af3b-177">To help with this, Azure offers several storage options such as blobs, tables, and SQL Database.</span></span> <span data-ttu-id="7af3b-178">Please see the [Data Storage Offerings in Azure][Data Storage Offerings in Azure] article for more information about these storage technologies.</span><span class="sxs-lookup"><span data-stu-id="7af3b-178">Please see the [Data Storage Offerings in Azure][Data Storage Offerings in Azure] article for more information about these storage technologies.</span></span> <span data-ttu-id="7af3b-179">The figure below shows how the load balancer inside the Azure data center distributes client requests to different role instances all of which have access to the same data storage.</span><span class="sxs-lookup"><span data-stu-id="7af3b-179">The figure below shows how the load balancer inside the Azure data center distributes client requests to different role instances all of which have access to the same data storage.</span></span>

![image][3]

<span data-ttu-id="7af3b-181">Usually, you want to locate your application code and your data in the same data center as this allows for low latency (better performance) when your application code accesses the data.</span><span class="sxs-lookup"><span data-stu-id="7af3b-181">Usually, you want to locate your application code and your data in the same data center as this allows for low latency (better performance) when your application code accesses the data.</span></span> <span data-ttu-id="7af3b-182">In addition, you are not charged for bandwidth when data is moved around within the same data center.</span><span class="sxs-lookup"><span data-stu-id="7af3b-182">In addition, you are not charged for bandwidth when data is moved around within the same data center.</span></span>

## <span data-ttu-id="7af3b-183"><a id="scale"> </a>Designing your Application for Scale</span><span class="sxs-lookup"><span data-stu-id="7af3b-183"><a id="scale"> </a>Designing your Application for Scale</span></span>
<span data-ttu-id="7af3b-184">Sometimes, you may want to take a single application (like a simple web site) and have it hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-184">Sometimes, you may want to take a single application (like a simple web site) and have it hosted in Azure.</span></span> <span data-ttu-id="7af3b-185">But frequently, your application may consist of several roles that all work together.</span><span class="sxs-lookup"><span data-stu-id="7af3b-185">But frequently, your application may consist of several roles that all work together.</span></span> <span data-ttu-id="7af3b-186">For example, in the figure below, there are two instances of the Website role, three instances of the Order Processing role, and one instance of the Report Generator role.</span><span class="sxs-lookup"><span data-stu-id="7af3b-186">For example, in the figure below, there are two instances of the Website role, three instances of the Order Processing role, and one instance of the Report Generator role.</span></span> <span data-ttu-id="7af3b-187">These roles are all working together and the code for all of them can be packaged together and deployed as a single unit up to Azure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-187">These roles are all working together and the code for all of them can be packaged together and deployed as a single unit up to Azure.</span></span>

![image][4]

<span data-ttu-id="7af3b-189">The main reason to split an application into different roles each running on its own set of role instances (that is, VMs) is to scale the roles independently.</span><span class="sxs-lookup"><span data-stu-id="7af3b-189">The main reason to split an application into different roles each running on its own set of role instances (that is, VMs) is to scale the roles independently.</span></span> <span data-ttu-id="7af3b-190">For example, during the holiday season, many customers may be purchasing products from your company, so you might want to increase the number of role instances running your Website role as well as the number of role instances running your Order Processing role.</span><span class="sxs-lookup"><span data-stu-id="7af3b-190">For example, during the holiday season, many customers may be purchasing products from your company, so you might want to increase the number of role instances running your Website role as well as the number of role instances running your Order Processing role.</span></span> <span data-ttu-id="7af3b-191">After the holiday season, you may get a lot of products returned, so you may still need a lot of Website instances but fewer Order Processing instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-191">After the holiday season, you may get a lot of products returned, so you may still need a lot of Website instances but fewer Order Processing instances.</span></span> <span data-ttu-id="7af3b-192">During the rest of the year, you may only need a few Website and Order Processing instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-192">During the rest of the year, you may only need a few Website and Order Processing instances.</span></span> <span data-ttu-id="7af3b-193">Throughout all of this, you may need only one Report Generator instance.</span><span class="sxs-lookup"><span data-stu-id="7af3b-193">Throughout all of this, you may need only one Report Generator instance.</span></span> <span data-ttu-id="7af3b-194">The flexibility of role-based deployments in Azure enables you to easily adapt your application to your business needs.</span><span class="sxs-lookup"><span data-stu-id="7af3b-194">The flexibility of role-based deployments in Azure enables you to easily adapt your application to your business needs.</span></span>

<span data-ttu-id="7af3b-195">It's common to have the role instances within your hosted service communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="7af3b-195">It's common to have the role instances within your hosted service communicate with each other.</span></span> <span data-ttu-id="7af3b-196">For example, the website role accepts a customer's order but then it offloads the order processing to the Order Processing role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-196">For example, the website role accepts a customer's order but then it offloads the order processing to the Order Processing role instances.</span></span> <span data-ttu-id="7af3b-197">The best way to pass work form one set of role instances to another set of instances is using the queuing technology provided by Azure, either the Queue Service or Service Bus Queues.</span><span class="sxs-lookup"><span data-stu-id="7af3b-197">The best way to pass work form one set of role instances to another set of instances is using the queuing technology provided by Azure, either the Queue Service or Service Bus Queues.</span></span> <span data-ttu-id="7af3b-198">The use of a queue is a critical part of the story here.</span><span class="sxs-lookup"><span data-stu-id="7af3b-198">The use of a queue is a critical part of the story here.</span></span> <span data-ttu-id="7af3b-199">The queue allows the hosted service to scale its roles independently allowing you to balance the workload against cost.</span><span class="sxs-lookup"><span data-stu-id="7af3b-199">The queue allows the hosted service to scale its roles independently allowing you to balance the workload against cost.</span></span> <span data-ttu-id="7af3b-200">If the number of messages in the queue increases over time, then you can scale up the number of Order Processing role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-200">If the number of messages in the queue increases over time, then you can scale up the number of Order Processing role instances.</span></span> <span data-ttu-id="7af3b-201">If the number of messages in the queue decreases over time, then you can scale down the number of Order Processing role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-201">If the number of messages in the queue decreases over time, then you can scale down the number of Order Processing role instances.</span></span> <span data-ttu-id="7af3b-202">This way, you are only paying for the instances required to handle the actual workload.</span><span class="sxs-lookup"><span data-stu-id="7af3b-202">This way, you are only paying for the instances required to handle the actual workload.</span></span>

<span data-ttu-id="7af3b-203">The queue also provides reliability.</span><span class="sxs-lookup"><span data-stu-id="7af3b-203">The queue also provides reliability.</span></span> <span data-ttu-id="7af3b-204">When scaling down the number of Order Processing role instances, Azure decides which instances to terminate.</span><span class="sxs-lookup"><span data-stu-id="7af3b-204">When scaling down the number of Order Processing role instances, Azure decides which instances to terminate.</span></span> <span data-ttu-id="7af3b-205">It may decide to terminate an instance that is in the middle of processing a queue message.</span><span class="sxs-lookup"><span data-stu-id="7af3b-205">It may decide to terminate an instance that is in the middle of processing a queue message.</span></span> <span data-ttu-id="7af3b-206">However, because the message processing does not complete successfully, the message becomes visible again to another Order Processing role instance that picks it up and processes it.</span><span class="sxs-lookup"><span data-stu-id="7af3b-206">However, because the message processing does not complete successfully, the message becomes visible again to another Order Processing role instance that picks it up and processes it.</span></span> <span data-ttu-id="7af3b-207">Because of queue message visibility, messages are guaranteed to eventually get processed.</span><span class="sxs-lookup"><span data-stu-id="7af3b-207">Because of queue message visibility, messages are guaranteed to eventually get processed.</span></span> <span data-ttu-id="7af3b-208">The queue also acts as a load balancer by effectively distributing its messages to any and all role instances that request messages from it.</span><span class="sxs-lookup"><span data-stu-id="7af3b-208">The queue also acts as a load balancer by effectively distributing its messages to any and all role instances that request messages from it.</span></span>

<span data-ttu-id="7af3b-209">For the Website role instances, you can monitor the traffic coming into them and decide to scale the number of them up or down as well.</span><span class="sxs-lookup"><span data-stu-id="7af3b-209">For the Website role instances, you can monitor the traffic coming into them and decide to scale the number of them up or down as well.</span></span> <span data-ttu-id="7af3b-210">The queue allows you to scale the number of Website role instances independently of the Order Processing role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-210">The queue allows you to scale the number of Website role instances independently of the Order Processing role instances.</span></span> <span data-ttu-id="7af3b-211">This is very powerful and gives you a lot of flexibility.</span><span class="sxs-lookup"><span data-stu-id="7af3b-211">This is very powerful and gives you a lot of flexibility.</span></span> <span data-ttu-id="7af3b-212">Of course, if your application consists of additional roles, you could add additional queues as the conduit to communicate between them in order to leverage the same scaling and cost benefits.</span><span class="sxs-lookup"><span data-stu-id="7af3b-212">Of course, if your application consists of additional roles, you could add additional queues as the conduit to communicate between them in order to leverage the same scaling and cost benefits.</span></span>

## <span data-ttu-id="7af3b-213"><a id="defandcfg"> </a>Hosted Service Definition and Configuration</span><span class="sxs-lookup"><span data-stu-id="7af3b-213"><a id="defandcfg"> </a>Hosted Service Definition and Configuration</span></span>
<span data-ttu-id="7af3b-214">Deploying a hosted service to Azure requires you to also have a service definition file and a service configuration file.</span><span class="sxs-lookup"><span data-stu-id="7af3b-214">Deploying a hosted service to Azure requires you to also have a service definition file and a service configuration file.</span></span> <span data-ttu-id="7af3b-215">Both of these files are XML files, and they allow you to declaratively specify deployment options for your hosted service.</span><span class="sxs-lookup"><span data-stu-id="7af3b-215">Both of these files are XML files, and they allow you to declaratively specify deployment options for your hosted service.</span></span> <span data-ttu-id="7af3b-216">The service definition file describes all of the roles that make up your hosted service and how they communicate.</span><span class="sxs-lookup"><span data-stu-id="7af3b-216">The service definition file describes all of the roles that make up your hosted service and how they communicate.</span></span> <span data-ttu-id="7af3b-217">The service configuration file describes the number of instances for each role and settings used to configure each role instance.</span><span class="sxs-lookup"><span data-stu-id="7af3b-217">The service configuration file describes the number of instances for each role and settings used to configure each role instance.</span></span>

## <span data-ttu-id="7af3b-218"><a id="def"> </a>The Service Definition File</span><span class="sxs-lookup"><span data-stu-id="7af3b-218"><a id="def"> </a>The Service Definition File</span></span>
<span data-ttu-id="7af3b-219">As I mentioned earlier, the service definition (CSDEF) file is an XML file that describes the various roles that make up your complete application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-219">As I mentioned earlier, the service definition (CSDEF) file is an XML file that describes the various roles that make up your complete application.</span></span> <span data-ttu-id="7af3b-220">The complete schema for the XML file can be found here: [http://msdn.microsoft.com/library/windowsazure/ee758711.aspx][].</span><span class="sxs-lookup"><span data-stu-id="7af3b-220">The complete schema for the XML file can be found here: [http://msdn.microsoft.com/library/windowsazure/ee758711.aspx][].</span></span>
<span data-ttu-id="7af3b-221">The CSDEF file contains a WebRole or WorkerRole element for each role that you want in your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-221">The CSDEF file contains a WebRole or WorkerRole element for each role that you want in your application.</span></span> <span data-ttu-id="7af3b-222">Deploying a role as a web role (using the WebRole element) means that the code will run on a role instance containing Windows Server 2008 and Internet Information Server (IIS).</span><span class="sxs-lookup"><span data-stu-id="7af3b-222">Deploying a role as a web role (using the WebRole element) means that the code will run on a role instance containing Windows Server 2008 and Internet Information Server (IIS).</span></span>
<span data-ttu-id="7af3b-223">Deploying a role as a worker role (using the WorkerRole element) means that the role instance will have Windows Server 2008 on it (IIS will not be installed).</span><span class="sxs-lookup"><span data-stu-id="7af3b-223">Deploying a role as a worker role (using the WorkerRole element) means that the role instance will have Windows Server 2008 on it (IIS will not be installed).</span></span>

<span data-ttu-id="7af3b-224">You can certainly create and deploy a worker role that uses some other mechanism to listen for incoming web requests (for example, your code could create and use a .NET HttpListener).</span><span class="sxs-lookup"><span data-stu-id="7af3b-224">You can certainly create and deploy a worker role that uses some other mechanism to listen for incoming web requests (for example, your code could create and use a .NET HttpListener).</span></span> <span data-ttu-id="7af3b-225">Since the role instances are all running Windows Server 2008, your code can perform any operations that are normally available to an application running on Windows Server</span><span class="sxs-lookup"><span data-stu-id="7af3b-225">Since the role instances are all running Windows Server 2008, your code can perform any operations that are normally available to an application running on Windows Server</span></span>
2008.

<span data-ttu-id="7af3b-226">For each role, you indicate the desired VM size that instances of that role should use.</span><span class="sxs-lookup"><span data-stu-id="7af3b-226">For each role, you indicate the desired VM size that instances of that role should use.</span></span> <span data-ttu-id="7af3b-227">The table below shows the various VM sizes available today and the attributes of each:</span><span class="sxs-lookup"><span data-stu-id="7af3b-227">The table below shows the various VM sizes available today and the attributes of each:</span></span>

<table border="2" cellspacing="0" cellpadding="5" style="border: 2px solid #000000;">

<tbody>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-228">
\*\*VM Size**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-228">
\*\*VM Size**

</span></span></td>

<td><span data-ttu-id="7af3b-229">
\*\*CPU**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-229">
\*\*CPU**

</span></span></td>

<td><span data-ttu-id="7af3b-230">
\*\*RAM**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-230">
\*\*RAM**

</span></span></td>

<td><span data-ttu-id="7af3b-231">
\*\*Disk**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-231">
\*\*Disk**

</span></span></td>

<td><span data-ttu-id="7af3b-232">
\*\*Peak Network I/O**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-232">
\*\*Peak Network I/O**

</span></span></td>
</tr>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-233">
\*\*Extra Small**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-233">
\*\*Extra Small**

</span></span></td>

<td>
<span data-ttu-id="7af3b-234">1 x 1.0 GHz</span><span class="sxs-lookup"><span data-stu-id="7af3b-234">1 x 1.0 GHz</span></span>

</td>

<td>
<span data-ttu-id="7af3b-235">768 MB</span><span class="sxs-lookup"><span data-stu-id="7af3b-235">768 MB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-236">20GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-236">20GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-237">\~5 Mbps</span><span class="sxs-lookup"><span data-stu-id="7af3b-237">\~5 Mbps</span></span>

</td>
</tr>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-238">
\*\*Small**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-238">
\*\*Small**

</span></span></td>

<td>
<span data-ttu-id="7af3b-239">1 x 1.6 GHz</span><span class="sxs-lookup"><span data-stu-id="7af3b-239">1 x 1.6 GHz</span></span>

</td>

<td>
<span data-ttu-id="7af3b-240">1.75 GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-240">1.75 GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-241">225GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-241">225GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-242">\~100 Mbps</span><span class="sxs-lookup"><span data-stu-id="7af3b-242">\~100 Mbps</span></span>

</td>
</tr>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-243">
\*\*Medium**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-243">
\*\*Medium**

</span></span></td>

<td>
<span data-ttu-id="7af3b-244">2 x 1.6 GHz</span><span class="sxs-lookup"><span data-stu-id="7af3b-244">2 x 1.6 GHz</span></span>

</td>

<td>
<span data-ttu-id="7af3b-245">3.5 GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-245">3.5 GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-246">490GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-246">490GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-247">\~200 Mbps</span><span class="sxs-lookup"><span data-stu-id="7af3b-247">\~200 Mbps</span></span>

</td>
</tr>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-248">
\*\*Large**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-248">
\*\*Large**

</span></span></td>

<td>
<span data-ttu-id="7af3b-249">4 x 1.6 GHz</span><span class="sxs-lookup"><span data-stu-id="7af3b-249">4 x 1.6 GHz</span></span>

</td>

<td>
<span data-ttu-id="7af3b-250">7 GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-250">7 GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-251">1TB</span><span class="sxs-lookup"><span data-stu-id="7af3b-251">1TB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-252">\~400 Mbps</span><span class="sxs-lookup"><span data-stu-id="7af3b-252">\~400 Mbps</span></span>

</td>
</tr>

<tr align="left" valign="top">

<td><span data-ttu-id="7af3b-253">
\*\*Extra Large**

</span><span class="sxs-lookup"><span data-stu-id="7af3b-253">
\*\*Extra Large**

</span></span></td>

<td>
<span data-ttu-id="7af3b-254">8 x 1.6 GHz</span><span class="sxs-lookup"><span data-stu-id="7af3b-254">8 x 1.6 GHz</span></span>

</td>

<td>
<span data-ttu-id="7af3b-255">14 GB</span><span class="sxs-lookup"><span data-stu-id="7af3b-255">14 GB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-256">2TB</span><span class="sxs-lookup"><span data-stu-id="7af3b-256">2TB</span></span>

</td>

<td>
<span data-ttu-id="7af3b-257">\~800 Mbps</span><span class="sxs-lookup"><span data-stu-id="7af3b-257">\~800 Mbps</span></span>

</td>
</tr>
</tbody>
</table>
<span data-ttu-id="7af3b-258">You are charged hourly for each VM you use as a role instance and you are also charged for any data that your role instances send outside the data center.</span><span class="sxs-lookup"><span data-stu-id="7af3b-258">You are charged hourly for each VM you use as a role instance and you are also charged for any data that your role instances send outside the data center.</span></span> <span data-ttu-id="7af3b-259">You are not charged for data entering the data center.</span><span class="sxs-lookup"><span data-stu-id="7af3b-259">You are not charged for data entering the data center.</span></span> <span data-ttu-id="7af3b-260">For more information, see [Azure Pricing][Azure Pricing].</span><span class="sxs-lookup"><span data-stu-id="7af3b-260">For more information, see [Azure Pricing][Azure Pricing].</span></span> <span data-ttu-id="7af3b-261">In general, it is advisable to use many small role instances as opposed to a few large instances so that your application is more resilient to failure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-261">In general, it is advisable to use many small role instances as opposed to a few large instances so that your application is more resilient to failure.</span></span> <span data-ttu-id="7af3b-262">After all, the fewer role instances you have, the more disastrous a failure in one of them is to your overall application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-262">After all, the fewer role instances you have, the more disastrous a failure in one of them is to your overall application.</span></span> <span data-ttu-id="7af3b-263">Also, as mentioned before, you must deploy at least two instances for each role in order to get the 99.95% service level agreement Microsoft provides.</span><span class="sxs-lookup"><span data-stu-id="7af3b-263">Also, as mentioned before, you must deploy at least two instances for each role in order to get the 99.95% service level agreement Microsoft provides.</span></span>

<span data-ttu-id="7af3b-264">The service definition (CSDEF) file is also where you would specify many attributes about each role in your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-264">The service definition (CSDEF) file is also where you would specify many attributes about each role in your application.</span></span> <span data-ttu-id="7af3b-265">Here are some of the more useful items available to you:</span><span class="sxs-lookup"><span data-stu-id="7af3b-265">Here are some of the more useful items available to you:</span></span>

* <span data-ttu-id="7af3b-266">**Certificates**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-266">**Certificates**.</span></span> <span data-ttu-id="7af3b-267">You use certificates for encrypting data or if your web service supports SSL.</span><span class="sxs-lookup"><span data-stu-id="7af3b-267">You use certificates for encrypting data or if your web service supports SSL.</span></span> <span data-ttu-id="7af3b-268">Any certificates need to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="7af3b-268">Any certificates need to be uploaded to Azure.</span></span> <span data-ttu-id="7af3b-269">For more information, see [Managing Certificates in Azure][Managing Certificates in Azure].</span><span class="sxs-lookup"><span data-stu-id="7af3b-269">For more information, see [Managing Certificates in Azure][Managing Certificates in Azure].</span></span> <span data-ttu-id="7af3b-270">This XML setting installs previously-uploaded certificates into the role instance's certificate store so that they are usable by your application code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-270">This XML setting installs previously-uploaded certificates into the role instance's certificate store so that they are usable by your application code.</span></span>
* <span data-ttu-id="7af3b-271">**Configuration Setting Names**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-271">**Configuration Setting Names**.</span></span> <span data-ttu-id="7af3b-272">For values that you want your application(s) to read while running on a role instance.</span><span class="sxs-lookup"><span data-stu-id="7af3b-272">For values that you want your application(s) to read while running on a role instance.</span></span> <span data-ttu-id="7af3b-273">The actual value of the configuration settings is set in the service configuration (CSCFG) file which can be updated at any time without requiring you to redeploy your code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-273">The actual value of the configuration settings is set in the service configuration (CSCFG) file which can be updated at any time without requiring you to redeploy your code.</span></span> <span data-ttu-id="7af3b-274">In fact, you can code your applications in such a way to detect the changed configuration values without incurring any downtime.</span><span class="sxs-lookup"><span data-stu-id="7af3b-274">In fact, you can code your applications in such a way to detect the changed configuration values without incurring any downtime.</span></span>
* <span data-ttu-id="7af3b-275">**Input Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-275">**Input Endpoints**.</span></span> <span data-ttu-id="7af3b-276">Here you specify any HTTP, HTTPS, or TCP endpoints (with ports) that you want to expose to the outside world via your *prefix*.cloadapp.net URL.</span><span class="sxs-lookup"><span data-stu-id="7af3b-276">Here you specify any HTTP, HTTPS, or TCP endpoints (with ports) that you want to expose to the outside world via your *prefix*.cloadapp.net URL.</span></span> <span data-ttu-id="7af3b-277">When Azure deploys your role, it will configure the firewall on the role instance automatically.</span><span class="sxs-lookup"><span data-stu-id="7af3b-277">When Azure deploys your role, it will configure the firewall on the role instance automatically.</span></span>
* <span data-ttu-id="7af3b-278">**Internal Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-278">**Internal Endpoints**.</span></span> <span data-ttu-id="7af3b-279">Here you specify any HTTP or TCP endpoints that you want exposed to other role instances that are deployed as part of your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-279">Here you specify any HTTP or TCP endpoints that you want exposed to other role instances that are deployed as part of your application.</span></span> <span data-ttu-id="7af3b-280">Internal endpoints allow all the role instances within your application to talk to each other but are not accessible to any role instances that are outside your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-280">Internal endpoints allow all the role instances within your application to talk to each other but are not accessible to any role instances that are outside your application.</span></span>
* <span data-ttu-id="7af3b-281">**Import Modules**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-281">**Import Modules**.</span></span> <span data-ttu-id="7af3b-282">These optionally install useful components on your role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-282">These optionally install useful components on your role instances.</span></span> <span data-ttu-id="7af3b-283">Components exist for diagnostic monitoring, remote desktop, and Azure Connect (which allows your role instance to access on-premises resources through a secure channel).</span><span class="sxs-lookup"><span data-stu-id="7af3b-283">Components exist for diagnostic monitoring, remote desktop, and Azure Connect (which allows your role instance to access on-premises resources through a secure channel).</span></span>
* <span data-ttu-id="7af3b-284">**Local Storage**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-284">**Local Storage**.</span></span> <span data-ttu-id="7af3b-285">This allocates a subdirectory on the role instance for your application to use.</span><span class="sxs-lookup"><span data-stu-id="7af3b-285">This allocates a subdirectory on the role instance for your application to use.</span></span> <span data-ttu-id="7af3b-286">It is described in more detail in the [Data Storage Offerings in Azure][Data Storage Offerings in Azure] article.</span><span class="sxs-lookup"><span data-stu-id="7af3b-286">It is described in more detail in the [Data Storage Offerings in Azure][Data Storage Offerings in Azure] article.</span></span>
* <span data-ttu-id="7af3b-287">**Startup Tasks**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-287">**Startup Tasks**.</span></span> <span data-ttu-id="7af3b-288">Startup tasks give you a way to install prerequisite components on a role instance as it boots up.</span><span class="sxs-lookup"><span data-stu-id="7af3b-288">Startup tasks give you a way to install prerequisite components on a role instance as it boots up.</span></span> <span data-ttu-id="7af3b-289">The tasks can run elevated as an administrator if required.</span><span class="sxs-lookup"><span data-stu-id="7af3b-289">The tasks can run elevated as an administrator if required.</span></span>

## <span data-ttu-id="7af3b-290"><a id="cfg"> </a>The Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="7af3b-290"><a id="cfg"> </a>The Service Configuration File</span></span>
<span data-ttu-id="7af3b-291">The service configuration (CSCFG) file is an XML file that describes settings that can be changed without redeploying your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-291">The service configuration (CSCFG) file is an XML file that describes settings that can be changed without redeploying your application.</span></span> <span data-ttu-id="7af3b-292">The complete schema for the XML file can be found here: [http://msdn.microsoft.com/library/windowsazure/ee758710.aspx][http://msdn.microsoft.com/library/windowsazure/ee758710.aspx].</span><span class="sxs-lookup"><span data-stu-id="7af3b-292">The complete schema for the XML file can be found here: [http://msdn.microsoft.com/library/windowsazure/ee758710.aspx][http://msdn.microsoft.com/library/windowsazure/ee758710.aspx].</span></span>
<span data-ttu-id="7af3b-293">The CSCFG file contains a Role element for each role in your application.</span><span class="sxs-lookup"><span data-stu-id="7af3b-293">The CSCFG file contains a Role element for each role in your application.</span></span> <span data-ttu-id="7af3b-294">Here are some of the items you can specify in the CSCFG file:</span><span class="sxs-lookup"><span data-stu-id="7af3b-294">Here are some of the items you can specify in the CSCFG file:</span></span>

* <span data-ttu-id="7af3b-295">**OS Version**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-295">**OS Version**.</span></span> <span data-ttu-id="7af3b-296">This attribute allows you to select the operating system (OS) version you want used for all the role instances running your application code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-296">This attribute allows you to select the operating system (OS) version you want used for all the role instances running your application code.</span></span> <span data-ttu-id="7af3b-297">This OS is known as the *guest OS*, and each new version includes the latest security patches and updates available at the time the guest OS is released.</span><span class="sxs-lookup"><span data-stu-id="7af3b-297">This OS is known as the *guest OS*, and each new version includes the latest security patches and updates available at the time the guest OS is released.</span></span> <span data-ttu-id="7af3b-298">If you set the osVersion attribute value to "\*", then Azure automatically updates the guest OS on each of your role instances as new guest OS versions become available.</span><span class="sxs-lookup"><span data-stu-id="7af3b-298">If you set the osVersion attribute value to "\*", then Azure automatically updates the guest OS on each of your role instances as new guest OS versions become available.</span></span> <span data-ttu-id="7af3b-299">However, you can opt out of automatic updates by selecting a specific guest OS version.</span><span class="sxs-lookup"><span data-stu-id="7af3b-299">However, you can opt out of automatic updates by selecting a specific guest OS version.</span></span> <span data-ttu-id="7af3b-300">For example, setting the osVersion attribute to a value of "WA-GUEST-OS-2.8\_201109-01" causes all your role instances to get what is described on this web page: [http://msdn.microsoft.com/library/hh560567.aspx][http://msdn.microsoft.com/library/hh560567.aspx].</span><span class="sxs-lookup"><span data-stu-id="7af3b-300">For example, setting the osVersion attribute to a value of "WA-GUEST-OS-2.8\_201109-01" causes all your role instances to get what is described on this web page: [http://msdn.microsoft.com/library/hh560567.aspx][http://msdn.microsoft.com/library/hh560567.aspx].</span></span> <span data-ttu-id="7af3b-301">For more information about guest OS versions, see [Managing Upgrades to the Azure Guests OS].</span><span class="sxs-lookup"><span data-stu-id="7af3b-301">For more information about guest OS versions, see [Managing Upgrades to the Azure Guests OS].</span></span>
* <span data-ttu-id="7af3b-302">**Instances**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-302">**Instances**.</span></span> <span data-ttu-id="7af3b-303">This element's value indicates the number of role instances you want provisioned running the code for a particular role.</span><span class="sxs-lookup"><span data-stu-id="7af3b-303">This element's value indicates the number of role instances you want provisioned running the code for a particular role.</span></span> <span data-ttu-id="7af3b-304">Since you can upload a new CSCFG file to Azure (without redeploying your application), it is trivially simple to change the value for this element and upload a new CSCFG file to dynamically increase or decrease the number of role instances running your application code.</span><span class="sxs-lookup"><span data-stu-id="7af3b-304">Since you can upload a new CSCFG file to Azure (without redeploying your application), it is trivially simple to change the value for this element and upload a new CSCFG file to dynamically increase or decrease the number of role instances running your application code.</span></span> <span data-ttu-id="7af3b-305">This allows you to easily scale your application up or down to meet actual workload demands while also controlling how much you are charged for running the role instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-305">This allows you to easily scale your application up or down to meet actual workload demands while also controlling how much you are charged for running the role instances.</span></span>
* <span data-ttu-id="7af3b-306">**Configuration Setting Values**.</span><span class="sxs-lookup"><span data-stu-id="7af3b-306">**Configuration Setting Values**.</span></span> <span data-ttu-id="7af3b-307">This element indicates values for settings (as defined in the CSDEF file).</span><span class="sxs-lookup"><span data-stu-id="7af3b-307">This element indicates values for settings (as defined in the CSDEF file).</span></span> <span data-ttu-id="7af3b-308">Your role can read these values while it is running.</span><span class="sxs-lookup"><span data-stu-id="7af3b-308">Your role can read these values while it is running.</span></span> <span data-ttu-id="7af3b-309">These configuration settings values are typically used for connection strings to SQL Database or to Azure Storage, but they can be used for any purpose you desire.</span><span class="sxs-lookup"><span data-stu-id="7af3b-309">These configuration settings values are typically used for connection strings to SQL Database or to Azure Storage, but they can be used for any purpose you desire.</span></span>

## <span data-ttu-id="7af3b-310"><a id="hostedservices"> </a>Creating and Deploying a Hosted Service</span><span class="sxs-lookup"><span data-stu-id="7af3b-310"><a id="hostedservices"> </a>Creating and Deploying a Hosted Service</span></span>
<span data-ttu-id="7af3b-311">Creating a hosted service requires that you first go to the [Azure Management Portal] and provision a hosted service by specifying a DNS prefix and the data center you ultimately want your code running in.</span><span class="sxs-lookup"><span data-stu-id="7af3b-311">Creating a hosted service requires that you first go to the [Azure Management Portal] and provision a hosted service by specifying a DNS prefix and the data center you ultimately want your code running in.</span></span> <span data-ttu-id="7af3b-312">Then in your development environment, you create your service definition (CSDEF) file, build your application code and package (zip) all these files into a service package (CSPKG) file.</span><span class="sxs-lookup"><span data-stu-id="7af3b-312">Then in your development environment, you create your service definition (CSDEF) file, build your application code and package (zip) all these files into a service package (CSPKG) file.</span></span> <span data-ttu-id="7af3b-313">You must also prepare your service configuration (CSCFG) file.</span><span class="sxs-lookup"><span data-stu-id="7af3b-313">You must also prepare your service configuration (CSCFG) file.</span></span> <span data-ttu-id="7af3b-314">To deploy your role, you upload the CSPKG and CSCFG files with the Azure Service Management API.</span><span class="sxs-lookup"><span data-stu-id="7af3b-314">To deploy your role, you upload the CSPKG and CSCFG files with the Azure Service Management API.</span></span> <span data-ttu-id="7af3b-315">Once deployed, Azure, will provision role instances in the data center (based upon the configuration data), extract your application code from the package, copy it to the role instances, and boot the instances.</span><span class="sxs-lookup"><span data-stu-id="7af3b-315">Once deployed, Azure, will provision role instances in the data center (based upon the configuration data), extract your application code from the package, copy it to the role instances, and boot the instances.</span></span> <span data-ttu-id="7af3b-316">Now, your code is up and running.</span><span class="sxs-lookup"><span data-stu-id="7af3b-316">Now, your code is up and running.</span></span>

<span data-ttu-id="7af3b-317">The figure below shows the CSPKG and CSCFG files you create on your development computer.</span><span class="sxs-lookup"><span data-stu-id="7af3b-317">The figure below shows the CSPKG and CSCFG files you create on your development computer.</span></span> <span data-ttu-id="7af3b-318">The CSPKG file contains the CSDEF file and the code for two roles.</span><span class="sxs-lookup"><span data-stu-id="7af3b-318">The CSPKG file contains the CSDEF file and the code for two roles.</span></span> <span data-ttu-id="7af3b-319">After uploading the CSPKG and CSCFG files with the Azure Service Management API, Azure creates the role instances in the data center.</span><span class="sxs-lookup"><span data-stu-id="7af3b-319">After uploading the CSPKG and CSCFG files with the Azure Service Management API, Azure creates the role instances in the data center.</span></span> <span data-ttu-id="7af3b-320">In this example, the CSCFG file indicated that Azure should create three instances of role \#1 and two instances of Role \#2.</span><span class="sxs-lookup"><span data-stu-id="7af3b-320">In this example, the CSCFG file indicated that Azure should create three instances of role \#1 and two instances of Role \#2.</span></span>

![image][5]

<span data-ttu-id="7af3b-322">For more information about deploying, upgrading, and reconfiguring your roles, see the [Deploying and Updating Azure Applications][Deploying and Updating Azure Applications] article.<a id="Ref" name="Ref"></a></span><span class="sxs-lookup"><span data-stu-id="7af3b-322">For more information about deploying, upgrading, and reconfiguring your roles, see the [Deploying and Updating Azure Applications][Deploying and Updating Azure Applications] article.<a id="Ref" name="Ref"></a></span></span>

## <span data-ttu-id="7af3b-323"><a id="references"> </a>References</span><span class="sxs-lookup"><span data-stu-id="7af3b-323"><a id="references"> </a>References</span></span>
* <span data-ttu-id="7af3b-324">[Creating a Hosted Service for Azure][Creating a Hosted Service for Azure]</span><span class="sxs-lookup"><span data-stu-id="7af3b-324">[Creating a Hosted Service for Azure][Creating a Hosted Service for Azure]</span></span>
* <span data-ttu-id="7af3b-325">[Managing Hosted Services in Azure][Managing Hosted Services in Azure]</span><span class="sxs-lookup"><span data-stu-id="7af3b-325">[Managing Hosted Services in Azure][Managing Hosted Services in Azure]</span></span>
* <span data-ttu-id="7af3b-326">[Migrating Applications to Azure][Migrating Applications to Azure]</span><span class="sxs-lookup"><span data-stu-id="7af3b-326">[Migrating Applications to Azure][Migrating Applications to Azure]</span></span>
* <span data-ttu-id="7af3b-327">[Configuring an Azure Application][Configuring an Azure Application]</span><span class="sxs-lookup"><span data-stu-id="7af3b-327">[Configuring an Azure Application][Configuring an Azure Application]</span></span>

<div style="width: 700px; border-top: solid; margin-top: 5px; padding-top: 5px; border-top-width: 1px;">

<p><span data-ttu-id="7af3b-328">Written by Jeffrey Richter (Wintellect)</span><span class="sxs-lookup"><span data-stu-id="7af3b-328">Written by Jeffrey Richter (Wintellect)</span></span></p>

</div>

[Azure Application Model Benefits]: #benefits
[Hosted Service Core Concepts]: #concepts
[Hosted Service Design Considerations]: #considerations
[Designing your Application for Scale]: #scale
[Hosted Service Definition and Configuration]: #defandcfg
[The Service Definition File]: #def
[The Service Configuration File]: #cfg
[Creating and Deploying a Hosted Service]: #hostedservices
[References]: #references
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-3.jpg
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-4.jpg
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-5.jpg
[Configuring a Custom Domain Name in Azure]: http://www.windowsazure.com/develop/net/common-tasks/custom-dns/
[Data Storage Offerings in Azure]: http://www.windowsazure.com/develop/net/fundamentals/cloud-storage/
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-6.jpg
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-7.jpg

[Azure Pricing]: http://www.windowsazure.com/pricing/calculator/
[Managing Certificates in Azure]: http://msdn.microsoft.com/library/windowsazure/gg981929.aspx
[http://msdn.microsoft.com/library/windowsazure/ee758710.aspx]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[http://msdn.microsoft.com/library/hh560567.aspx]: http://msdn.microsoft.com/library/hh560567.aspx
[Managing Upgrades to the Azure Guests OS]: http://msdn.microsoft.com/library/ee924680.aspx
[Azure Management Portal]: http://manage.windowsazure.com/
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/application-model/application-model-8.jpg
[Deploying and Updating Azure Applications]: http://www.windowsazure.com/develop/net/fundamentals/deploying-applications/
[Creating a Hosted Service for Azure]: http://msdn.microsoft.com/library/gg432967.aspx
[Managing Hosted Services in Azure]: http://msdn.microsoft.com/library/gg433038.aspx
[Migrating Applications to Azure]: http://msdn.microsoft.com/library/gg186051.aspx
[Configuring an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405486.aspx






