## <a name="virtual-network-basics"></a>Virtual Network Basics
### <a name="what-is-an-azure-virtual-network-vnet"></a>What is an Azure Virtual network (VNet)?
You can use VNets to provision and manage virtual private networks (VPNs) in Azure and, optionally, link the VNets with other VNets in Azure, or with your on-premises IT infrastructure to create hybrid or cross-premises solutions. Each VNet you create has its own CIDR block, and can be linked to other VNets and on-premises networks as long as the CIDR blocks do not collide. You also have controls of DNS server settings for VNets, and segmentation of the VNet into subnets.

Use VNets to:

* Create a dedicated private cloud-only virtual network
  
    Sometimes you don't require a cross-premises configuration for your solution. When you create a VNet, your services and VMs within your VNet can communicate directly and securely with each other in the cloud. This keeps traffic securely within the VNet, but still allows you to configure endpoint connections for the VMs and services that require Internet communication as part of your solution.
* Securely extend your data center
  
    With VNets, you can build traditional site-to-site (S2S) VPNs to securely scale your datacenter capacity. S2S VPNs use IPSEC to provide a secure connection between your corporate VPN gateway and Azure.
* Enable hybrid cloud scenarios
  
    VNets give you the flexibility to support a range of hybrid cloud scenarios. You can securely connect cloud-based applications to any type of on-premises system such as mainframes and Unix systems.

### <a name="how-do-i-know-if-i-need-a-virtual-network"></a>How do I know if I need a virtual network?
Visit the [Virtual Network Overview](../articles/virtual-network/virtual-networks-overview.md) to see a decision table that will help you decide the best network design option for you.

### <a name="how-do-i-get-started"></a>How do I get started?
Visit [the Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/) to get started. This page has links to common configuration steps as well as information that will help you understand the things that you'll need to take into consideration when designing your virtual network.

### <a name="what-services-can-i-use-with-vnets"></a>What services can I use with VNets?
VNets can be used with a variety of different Azure services, such as Cloud Services (PaaS), Virtual Machines, and Web Apps. However, there are a few services that are not supported on a VNet. Please check the specific service you want to use and verify that it is compatible.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Can I use VNets without cross-premises connectivity?
Yes. You can use a VNet without using site-to-site connectivity. This is particularly useful if you want to run domain controllers and SharePoint farms in Azure.

## <a name="virtual-network-configuration"></a>Virtual Network Configuration
### <a name="what-tools-do-i-use-to-create-a-vnet"></a>What tools do I use to create a VNet?
You can use the following tools to create or configure a virtual network:

* Azure Portal (for classic and Resource Manager VNets).
* A network configuration file (netcfg - for classic VNets only). See [Configure a virtual network using a network configuration file](../articles/virtual-network/virtual-networks-using-network-configuration-file.md).
* PowerShell (for classic and Resource Manager VNets).
* Azure CLI (for classic and Resource Manager VNets).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>What address ranges can I use in my VNets?
You can use public IP address ranges and any IP address range defined in [RFC 1918](http://tools.ietf.org/html/rfc1918).

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>Can I have public IP addresses in my VNets?
Yes. For more information about public IP address ranges, see [Public IP address space in a Virtual Network (VNet)](../articles/virtual-network/virtual-networks-public-ip-within-vnet.md). Keep in mind that your public IPs will not be directly accessible from the Internet.

### <a name="is-there-a-limit-to-the-number-of-subnets-in-my-virtual-network"></a>Is there a limit to the number of subnets in my virtual network?
There is no limit on the number of subnets you use within a VNet. All the subnets must be fully contained in the virtual network address space and should not overlap with one another.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Are there any restrictions on using IP addresses within these subnets?
Azure reserves some IP addresses within each subnet. The first and last IP addresses of the subnets are reserved for protocol conformance, along with 3 more addresses used for Azure services.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>How small and how large can VNets and subnets be?
The smallest subnet we support is a /29 and the largest is a /8 (using CIDR subnet definitions).

### <a name="can-i-bring-my-vlans-to-azure-using-vnets"></a>Can I bring my VLANs to Azure using VNets?
No. VNets are Layer-3 overlays. Azure does not support any Layer-2 semantics.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Can I specify custom routing policies on my VNets and subnets?
Yes. You can use User Defined Routing (UDR). For more information about UDR, visit [User Defined Routes and IP Forwarding](../articles/virtual-network/virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Do VNets support multicast or broadcast?
No. We do not support multicast or broadcast.

### <a name="what-protocols-can-i-use-within-vnets"></a>What protocols can I use within VNets?
You can use standard IP-based protocols within VNets. However, multicast, broadcast, IP-in-IP encapsulated packets and Generic Routing Encapsulation (GRE) packets are blocked within VNets. Standard protocols that work include:

* TCP
* UDP
* ICMP

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Can I ping my default routers within a VNet?
No.

### <a name="can-i-use-tracert-to-diagnose-connectivity"></a>Can I use tracert to diagnose connectivity?
No.

### <a name="can-i-add-subnets-after-the-vnet-is-created"></a>Can I add subnets after the VNet is created?
Yes. Subnets can be added to VNets at any time as long as the subnet address is not part of another subnet in the VNet.

### <a name="can-i-modify-the-size-of-my-subnet-after-i-create-it"></a>Can I modify the size of my subnet after I create it?
You can add, remove, expand or shrink a subnet if there are no VMs or services deployed within it by using PowerShell cmdlets or the NETCFG file. You can also add, remove, expand or shrink any prefixes as long as the subnets that contain VMs or services are not affected by the change.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Can I modify subnets after I created them?
Yes. You can add, remove, and modify the CIDR blocks used by a VNet.

### <a name="can-i-connect-to-the-internet-if-i-am-running-my-services-in-a-vnet"></a>Can I connect to the internet if I am running my services in a VNet?
Yes. All services deployed within a VNet can connect to the internet. Every cloud service deployed in Azure has a publicly addressable VIP assigned to it. You will have to define input endpoints for PaaS roles and endpoints for virtual machines to enable these services to accept connections from the internet.

### <a name="do-vnets-support-ipv6"></a>Do VNets support IPv6?
No. You cannot use IPv6 with VNets at this time.

### <a name="can-a-vnet-span-regions"></a>Can a VNet span regions?
No. A VNet is limited to a single region.

### <a name="can-i-connect-a-vnet-to-another-vnet-in-azure"></a>Can I connect a VNet to another VNet in Azure?
Yes. You can create VNet to VNet communication by using REST APIs or Windows PowerShell. You can also connect VNets via VNet Peering. See more details about peering [here.](../articles/virtual-network/virtual-network-peering-overview.md)

## <a name="name-resolution-dns"></a>Name Resolution (DNS)
### <a name="what-are-my-dns-options-for-vnets"></a>What are my DNS options for VNets?
Use the decision table on the [Name Resolution for VMs and Role Instances](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) page to guide you through all the DNS options available.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>Can I specify DNS servers for a VNet?
Yes. You can specify DNS server IP addresses in the VNet settings. This will be applied as the default DNS server(s) for all VMs in the VNet.

### <a name="how-many-dns-servers-can-i-specify"></a>How many DNS servers can I specify?
You can specify up to 12 DNS servers.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-the-network"></a>Can I modify my DNS servers after I have created the network?
Yes. You can change the DNS server list for your VNet at any time. If you change your DNS server list, you will need to restart each of the VMs in your VNet in order for them to pick up the new DNS server.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>What is Azure-provided DNS and does it work with VNets?
Azure-provided DNS is a multi-tenant DNS service offered by Microsoft. Azure registers all of your VMs and role instances in this service. This service provides name resolution by hostname for VMs and role instances contained within the same cloud service, and by FQDN for VMs and role instances in the same VNet.

> [!NOTE]
> There is a limitation at this time to the first 100 cloud services in the virtual network for cross-tenant name resolution using Azure-provided DNS. If you are using your own DNS server, this limitation does not apply.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Can I override my DNS settings on a per-VM / service basis?
Yes. You can set DNS servers on a per-cloud service basis to override the default network settings. However, we recommend that you use network-wide DNS as much as possible.

### <a name="can-i-bring-my-own-dns-suffix"></a>Can I bring my own DNS suffix?
No. You cannot specify a custom DNS suffix for your VNets.

## <a name="vnets-and-vms"></a>VNets and VMs
### <a name="can-i-deploy-vms-to-a-vnet"></a>Can I deploy VMs to a VNet?
Yes.

### <a name="can-i-deploy-linux-vms-to-a-vnet"></a>Can I deploy Linux VMs to a VNet?
Yes. You can deploy any distro of Linux supported by Azure.

### <a name="what-is-the-difference-between-a-public-vip-and-an-internal-ip-address"></a>What is the difference between a public VIP and an internal IP address?
* An internal IP address is an IP address that is assigned to each VM within a VNet by DHCP. It's not public facing. If you have created a VNet, the internal IP address is assigned from the range that you specified in the subnet settings of your VNet. If you do not have a VNet, an internal IP address will still be assigned. The internal IP address will remain with the VM for its lifetime, unless that VM is deallocated.
* A public VIP is the public IP address that is assigned to your cloud service or load balancer. It is not assigned directly to your VM NIC. The VIP stays with the cloud service it is assigned to until all the VMs in that cloud service are deallocated or deleted. At that point, it is released.

### <a name="what-ip-address-will-my-vm-receive"></a>What IP address will my VM receive?
* **Internal IP address -** If you deploy a VM to a VNet, the VM receives an internal IP address from a pool of internal IP addresses that you specify. VMs communicate within the VNets by using internal IP addresses. Although Azure assigns a dynamic internal IP address, you can request a static address for your VM. To learn more about static internal IP addresses, visit [How to Set a Static Internal IP](../articles/virtual-network/virtual-networks-reserved-private-ip.md).
* **VIP -** Your VM is also associated with a VIP, although a VIP is never assigned to the VM directly. A VIP is a public IP address that can be assigned to your cloud service. You can, optionally, reserve a VIP for your cloud service.
* **ILPIP -** You can also configure an instance-level public IP address (ILPIP). ILPIPs are directly associated with the VM, rather than the cloud service. To learn more about ILPIPs, visit [Instance-Level Public IP Overview](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).

### <a name="can-i-reserve-an-internal-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Can I reserve an internal IP address for a VM that I will create at a later time?
No. You cannot reserve an internal IP address. If an internal IP address is available it will be assigned to a VM or role instance by the DHCP server. That VM may or may not be the one that you want the internal IP address to be assigned to. You can, however, change the internal IP address of an already created VM to any available internal IP address.

### <a name="do-internal-ip-addresses-change-for-vms-in-a-vnet"></a>Do internal IP addresses change for VMs in a VNet?
Yes. Internal IP addresses remain with the VM for its lifetime unless the VM is deallocated. When a VM is deallocated, the internal IP address is released unless you defined a static internal IP address for your VM. If the VM is simply stopped (and not put in the status **Stopped (Deallocated)**) the IP address will remain assigned to the VM.

### <a name="can-i-manually-assign-ip-addresses-to-nics-in-vms"></a>Can I manually assign IP addresses to NICs in VMs?
No. You must not change any interface properties of VMs. Any changes may lead to potentially losing connectivity to the VM.

### <a name="what-happens-to-my-ip-addresses-if-i-shut-down-a-vm"></a>What happens to my IP addresses if I shut down a VM?
Nothing. The IP addresses (both public VIP and internal IP address) will stay with your cloud service or VM.

> [!NOTE]
> If you want to simply shut down the VM, don't use the Management Portal to do so. Currently, the shutdown button will deallocate the virtual machine.
> 
> 

### <a name="can-i-move-vms-from-one-subnet-to-another-subnet-in-a-vnet-without-re-deploying"></a>Can I move VMs from one subnet to another subnet in a VNet without re-deploying?
Yes. You can find more information [here](../articles/virtual-network/virtual-networks-move-vm-role-to-subnet.md).

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>Can I configure a static MAC address for my VM?
No. A MAC address cannot be statically configured.

### <a name="will-the-mac-address-remain-the-same-for-my-vm-once-it-has-been-created"></a>Will the MAC address remain the same for my VM once it has been created?
Yes, the MAC address will remain the same for a VM even though the VM has been stopped (deallocated) and relaunched.

### <a name="can-i-connect-to-the-internet-from-a-vm-in-a-vnet"></a>Can I connect to the internet from a VM in a VNet?
Yes. All services deployed within a VNet can connect to the Internet. Additionally, every cloud service deployed in Azure has a publicly addressable VIP assigned to it. You have to define input endpoints for PaaS roles and endpoints for VMs to enable these services to accept connections from the Internet.

## <a name="vnets-and-services"></a>VNets and Services
### <a name="what-services-can-i-use-with-vnets"></a>What services can I use with VNets?
You can only use compute services within VNets. Compute services are limited to Cloud Services (web and worker roles) and VMs.

### <a name="can-i-use-web-apps-with-virtual-network"></a>Can I use Web Apps with Virtual Network?
Yes. You can deploy Web Apps inside a VNet using ASE (App Service Environment). Adding to that, Web Apps can securely connect and access resources in your Azure VNet if you have point-to-site configured for your VNet. For more information, see the following:

* [Creating Web Apps in an App Service Environment](../articles/app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Web Apps Virtual Network Integration](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)
* [Using VNet Integration and Hybrid Connections with Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)
* [Integrate a web app with an Azure Virtual Network](../articles/app-service-web/web-sites-integrate-with-vnet.md)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Can I deploy cloud services with web and worker roles (PaaS) in a VNet?
Yes. You can deploy PaaS services within VNets.

### <a name="how-do-i-deploy-paas-roles-to-a-vnet"></a>How do I deploy PaaS roles to a VNet?
You can accomplish this by specifying the VNet name and the role /subnet mappings in the network configuration section of your service configuration. You do not need to update any of your binaries.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Can I move my services in and out of VNets?
No. You cannot move services in and out of VNets. You will have to delete and re-deploy the service to move it to another VNet.

## <a name="vnets-and-security"></a>VNets and Security
### <a name="what-is-the-security-model-for-vnets"></a>What is the security model for VNets?
VNets are completely isolated from one another, and other services hosted in the Azure infrastructure. A VNet is a trust boundary.

### <a name="can-i-define-acls-or-nsgs-on-my-vnets"></a>Can I define ACLs or NSGs on my VNets?
No. You cannot associate ACLs or NSGs to VNets. However, ACLs can be defined on input endpoints for VMs that have been deployed to a VNets, and NSGs can be associated to subnets or NICs.

### <a name="is-there-a-vnet-security-whitepaper"></a>Is there a VNet security whitepaper?
Yes. You can download it [here](http://go.microsoft.com/fwlink/?LinkId=386611).

## <a name="apis-schemas-and-tools"></a>APIs, Schemas, and Tools
### <a name="can-i-manage-vnets-from-code"></a>Can I manage VNets from code?
Yes. You can use REST APIs to manage VNets and cross-premises connectivity. More information can be found [here](http://go.microsoft.com/fwlink/?LinkId=296833).

### <a name="is-there-tooling-support-for-vnets"></a>Is there tooling support for VNets?
Yes. You can use PowerShell and command line tools for a variety of platforms. More information can be found [here](http://go.microsoft.com/fwlink/?LinkId=317721).

