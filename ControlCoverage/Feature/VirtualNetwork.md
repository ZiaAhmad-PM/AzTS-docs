## Virtual Network

| ControlId | Dependent Azure API(s) and Properties | Control spec-let |
|-----------|-------------------------------------|------------------|
| <b>ControlId:</b><br>Azure_ERvNet_NetSec_Dont_Add_UDRs_on_Subnets<br><b>DisplayName:</b><br>There must not be a UDR on *any* subnet in an ExpressRoute-connected vNet.<br><b>Description: </b><br> There must not be a UDR on *any* subnet in an ExpressRoute-connected vNet.| <br><b>ARM API to list Virtual Networks and route table associated with each subnet of vNet at subscription level: </b> <br> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworks?<br>api-version=2019-11-01 <br><b>Properties:</b><br> properties.subnets[\*].properties.routeTable.id <br><br><b>ARM API to list Virtual Network Gateways at subscription level: </b> <br> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworkGateways?<br>api-version=2019-04-01 <br><b>Properties:</b><br>Properties.gatewayType <br><br><b> ARM API to list all Route Tables at subscription level: </b> <br> /subscriptions/{subscriptionId}/providers/Microsoft.Network/routeTables?api-version=2020-03-01 <br><b>Properties:</b><br> Properties.routes[\*].name <br> Properties.routes[\*].properties.addressPrefix <br> Properties.routes[\*].properties.nextHopType| <b>Passed: </b><br>1. No UDRs found on any Subnet of ERvNet. <br> 2. Only exempted UDR(s) are defined in subnet of ERvNet.<br><b>Failed: </b><br> UDRs are attached to one or more subntes in ERvNet. <br><b>NotApplicable: </b><br>Current VNet resource object is not connected to ExpressRoute gateway. |
| <b>ControlId:</b><br>Azure_ERvNet_NetSec_Dont_Use_VNet_Peerings<br><b>DisplayName:</b><br>Peering must not be allowed on ExpressRoute connected Virtual Network. <br><b>Description: </b><br> There must not be any virtual network peerings on an ExpressRoute-connected vNet.| <b> ARM API to list Virtual Networks and their peerings at subscription level: </b> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworks? <br> api-version=2019-11-01 <br><b>Properties:</b><br> Properties.virtualNetworkPeerings[\*].id <br> Properties.virtualNetworkPeerings[\*].properties.remoteVirtualNetwork.id <br> <br> <b> ARM API to list Virtual Network Gateways at subscription level: </b> <br> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworkGateways?<br>api-version=2019-04-01 <br><b>Properties:</b><br> Properties.gatewayType | <b>Passed: </b><br>No peerings found on ERvNet. <br> Only exempted peerings are defined in ERvNet.<br><b>Failed: </b><br>One or more non exempted peerings found on ERvNet. <br><b>NotApplicable: </b><br> Current VNet resource object is not connected to ExpressRoute gateway. |
| <b>ControlId:</b><br>Azure_ERvNet_NetSec_Dont_Add_VPN_Gateways<br><b>DisplayName:</b><br> There must not be another virtual network gateway (GatewayType = Vpn) in an ExpressRoute-connected vNet. <br><b>Description: </b><br> There must not be another virtual network gateway (GatewayType = Vpn) in an ExpressRoute-connected vNet.| <b> ARM API to list Virtual Networks and their subnets at subscription level: </b> <br> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworks? <br>api-version=2019-11-01 <br><b>Properties:</b><br> properties.subnets[\*].id <br><br> <b> ARM API to list Virtual Network Gateways at subscription level: </b> /subscriptions/{subscriptionId}/providers/Microsoft.Network/virtualNetworkGateways?</br> api-version=2019-04-01 <br><b>Properties:</b><br> Properties.gatewayType | <b>Passed: </b><br>No other types of gateways found on the vNet other than ExpressRoute.<br><b>Failed: </b><br>Gateways of type other than ExpressRoute are found on the vNet.<br><b>NotApplicable: </b><br>Current VNet resource object is not connected to ExpressRoute gateway. |

