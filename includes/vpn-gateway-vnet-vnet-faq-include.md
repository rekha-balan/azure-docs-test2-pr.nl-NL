###<a name="does-azure-charge-for-traffic-between-vnets"></a>Does Azure charge for traffic between VNets?
VNet-to-VNet traffic within the same region is free for both directions. Cross region VNet-to-VNet egress traffic is charged with the outbound inter-VNet data transfer rates based on the source regions. Refer to the [pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.

###<a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a>Does VNet-to-VNet traffic travel across the Internet?
No. VNet-to-VNet traffic travels across the Microsoft Azure backbone, not the Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Is VNet-to-VNet traffic secure?
Yes, it is protected by IPsec/IKE encryption.

###<a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a>Do I need a VPN device to connect VNets together?
No. Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.

###<a name="do-my-vnets-need-to-be-in-the-same-region"></a>Do my VNets need to be in the same region?
No. The virtual networks can be in the same or different Azure regions (locations).

###<a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Can I use VNet-to-VNet along with multi-site connections?
Yes. Virtual network connectivity can be used simultaneously with multi-site VPNs.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>How many on-premises sites and virtual networks can one virtual network connect to?
See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.

###<a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a>Can I use VNet-to-VNet to connect VMs or cloud services outside of a VNet?
No. VNet-to-VNet supports connecting virtual networks. It does not support connecting virtual machines or cloud services that are not in a virtual network.

###<a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Can a cloud service or a load balancing endpoint span VNets?
No. A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.

###<a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?
No. VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a>Can I connect a VNet with a RouteBased VPN Type to another VNet with a PolicyBased VPN type?
No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.

###<a name="do-vpn-tunnels-share-bandwidth"></a>Do VPN tunnels share bandwidth?
Yes. All VPN tunnels of the virtual network share the available bandwidth on the Azure VPN gateway and the same VPN gateway uptime SLA in Azure.

###<a name="are-redundant-tunnels-supported"></a>Are redundant tunnels supported?
Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.

###<a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Can I have overlapping address spaces for VNet-to-VNet configurations?
No. You can't have overlapping IP address ranges.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Can there be overlapping address spaces among connected virtual networks and on-premises local sites?
No. You can't have overlapping IP address ranges.



