# azure-vnet-peering

Demonstration of configuring peering between two VNets in Azure

## Getting Started

An Azure RM template is included in `infrastructure/` to create the environment:

<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Flrakai%2Fazure-vnet-peering%2Fmaster%2Finfrastructure%2Farm-template.json">
    <img src="https://camo.githubusercontent.com/536ab4f9bc823c2e0ce72fb610aafda57d8c6c12/687474703a2f2f61726d76697a2e696f2f76697375616c697a65627574746f6e2e706e67" data-canonical-src="http://armviz.io/visualizebutton.png" style="max-width:100%;">
</a> 

Using Azure PowerShell, do the following to provision the resources:

```ps1
.\startup.ps1
```

Alternatively, you can perform a one-click deploy with the following button:

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Flrakai%2Fazure-vnet-peering%2Fmaster%2Finfrastructure%2Farm-template.json">
    <img src="https://camo.githubusercontent.com/9285dd3998997a0835869065bb15e5d500475034/687474703a2f2f617a7572656465706c6f792e6e65742f6465706c6f79627574746f6e2e706e67" data-canonical-src="http://azuredeploy.net/deploybutton.png" style="max-width:100%;">
</a>

## Following Along

1. Create a Linux VM with password authentication in a new VNet called _dev_. The VNet can be in a different region although peering data transfer costs are higher than if VNets are in the same region.
1. Initiate a peering connection from the _shared-vnet_ VNet with the _dev_ VNet. Observe the status of the peering is _Initiated_. The peering connection cannot be used until the status is _Connected_.
1. Initiate a peering connection from the dev_ VNet with the _shared-vnet_ VNet. Observe the status of the peering is _Connected_. The peering connection cannot be used until the status is _Connected_.
1. Use the serial console of the VM in the dev VNet to connect the the VM in the shared VNet using a private IP address:

    ```sh
    ssh 10.0.0.100
    ```
    This confirms the peering connection allows traffic between VNets using Azure's private backbone network (not the public internet).

## Tearing Down

When finished, remove the Azure resources with:

```ps1
.\teardown.ps1
```