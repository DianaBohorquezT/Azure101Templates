# Basic Landing Zone for POC

The following template will help you deploy the minimal resources you need for doing an Azure POC of a workload that needs to be connected to ONPREM network. Examples of the workloads that can be tested with this template are:

- Windows 365 Enterprise
- Storage accounts / Netapp SMB files that need authentication with the Active Directory onprem
- Join a virtual machine on the cloud to onprem Active Directory for management. 

Keep in mind this template is intended just for a quick test and it is expected for you to delete the resources. Once the pilot is completed, a discussion about [Cloud Adoption Framework](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/) needs to happen in order to account for best practices and have a well-architected Azure environment.

## Prerequisits

Since the template will create a VPN connection to ONPREM, it is necessary to have someone who knows about your network on this conversation. This person will need to:

- Provide an address space for Azure that will not overlap with current ONPREM environment. We have selected one by default, but you can customize it if needed
- Decide an Edge device to be connected to: We need the public IP fo this device and the address space that you intend to reach onprem.
- Select key (password) that both Azure VPN and ONPREM VPN will share to recognize each other
- Once the deployment is ready on Azure, this person will need to configure the onprem connection side

## Deployed Resources

This template deploys:

- A virtual network that has three subnets: GatewaySubnet, AzureBastionSubnet, VirtualMachineSubnet
- Virtual Network Gateway on Basic SKU which will be the terminating device on Azure environment. Click [here](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways) to read more information about VPN Gateway.
- A Local Network Gateway that will represent your edge device ONPREM. Read more about Local Network Gateway [here](https://docs.microsoft.com/en-us/azure/vpn-gateway/tutorial-site-to-site-portal#:~:text=The%20local%20network%20gateway%20is,the%20site)%20for%20routing%20purposes.)
- An Azure Bastion that is a secure jumpbox for you to connect to the virtual machines deployed on VirtualMachineSubnet. Click [here](https://docs.microsoft.com/en-us/azure/bastion/bastion-overview) to read more about Azure Bastion.
- A Windows virtual machine that will serve to test the connection between Azure and ONPREM.

## Steps to follow in order to deploy successfully

Click on the following button to open the template:

[![Deploy To Azure](https://docs.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDianaBohorquezT%2FAzure101Templates%2Fmain%2FlandingZoneLiteTemplate.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FDianaBohorquezT%2FAzure101Templates%2Fmain%2FlandingZoneLiteUI.json)

Complete the template parameters in order to deploy. Once the deployment has finished you can follow the next steps:

1. Give your network engineer the following information in order to connect from ONPREM
 - **Public IP of your gateway** Search on the Search bar for "azure-poc-vnetgw", click on the resource and on the overview tab you should be able to see the Public IP at the bottom of the second column like the following image shows:
   <img src=images/VPNGWpip.PNG/>

- **The address space of the created VNET** Search for azure-poc-vnet on the Azure Search Bar. Open the Virtual Network and click on Address Space tab. You should be able to see what is the address space here as the following image shows
  <img src=images/vnetAddSp.PNG/>

-**The Shared Key** If you forgot what you choose during the deployment, or want to change it search for azure-poc-vpnconnection connection and choose Shared Key Tab on the left to retrieve the information. DO NOT share this key with anyone outside your organization. The following image is just illustrative and is not a real key on any environment:

 <img src=images/sharedKey.PNG/>
