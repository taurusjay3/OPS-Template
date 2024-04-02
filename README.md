# OPS-Template

{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "functions": [],
    "variables": {
        "Vnet": "Virtual_Network_LABS",
        "Subnet-1": "Backend",
        "Subnet-2": "Frontend",
        "Subnet-3": "Database"


    },
    "resources": [

        {
            "name": "Allow_NSG_Frontend",
            "type": "Microsoft.Network/networkSecurityGroups",
            "apiVersion": "2020-11-01",
            "location": "[resourceGroup().location]",
            "properties": {
                "securityRules": [
                    {
                        "name": "nsgRuleA",
                        "properties": {
                            "description": "ALLOW TRAFFIC ON PORT 80",
                            "protocol": "Tcp",
                            "sourcePortRange": "*",
                            "destinationPortRange": "80",
                            "sourceAddressPrefix": "*",
                            "destinationAddressPrefix": "192.168.0.0/16",
                            "access": "Allow",
                            "priority": 100,
                            "direction": "Inbound"
                        }
                    },

                    {
                        "name": "nsgRuleB",
                        "properties": {
                            "description": "ALLOW TRAFFIC ON PORT 22",
                            "protocol": "Tcp",
                            "sourcePortRange": "*",
                            "destinationPortRange": "22",
                            "sourceAddressPrefix": "*",
                            "destinationAddressPrefix": "192.168.0.0/16",
                            "access": "Deny",
                            "priority": 100,
                            "direction": "Inbound"
                        }
                    }
                ]
            }
        },


       {
        "name": "[variables('Vnet')]",
        "type": "Microsoft.Network/virtualNetworks",
        "apiVersion": "2020-11-01",
        "location": "[resourceGroup().location]",
        "tags": {
            "displayName": "OPS_LABS"
        },
        "properties": {
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "[variables('Subnet-1')]",
                    "properties": {
                        "addressPrefix": "192.168.0.4"
                    }
                },
                {
                    "name": "[variables('Subnet-2')]",
                    "properties": {
                        "addressPrefix": "192.168.0.5"
                    }
                    
                },
                {
                    "name": "[variables('Subnet-3')]",
                    "properties": {
                        "addressPrefix": "192.168.0.6"
                    }
                }
            ]
        }
       }

    ],
    "outputs": {}
}
