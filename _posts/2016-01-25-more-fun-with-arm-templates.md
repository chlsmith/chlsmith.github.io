---
layout: post
title: More Fun with ARM Templates
date: 2016-01-25 12:28


categories: [Uncategorized]
---
All this time, all I've wanted to do with an Azure Resource Manager (ARM) template was create a bunch of identical computers.   The biggest roadblock I've faced is figuring out how to make the ARM template not one gigantic document with similarly-named resources in it.

Each VM requires a public IP address, a NIC, and a VM resource.   When I've put those into a template, if I named everything to make sense to me (like "Computer1" would have "Computer1-IP" and "Computer1-NIC" attached to it), the document gets really hard to follow.    I can copy and paste the definitions for these three objects, but eventually it gets ugly and confusing, and when something doesn't work, it's a pain to work around.

Enter the "count" parameter!   There's a neat way that you can tell the ARM engine to iterate through a list of resources and create however many you want it to.   The engine breaks down the JSON file and duplicates the guts of it "n" times, assigning a suffix with the number on it at the end of the item names.

Below is my ARM template that creates as many VMs as you want, each with a public IP address and a NIC.

---------------------
<h5><em>{</em>
<em> "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",</em>
<em> "contentVersion": "1.0.0.0",</em>
<em> "parameters": {</em>
<em> "userImageStorageAccountName": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "This is the name of the your storage account"</em>
<em> }</em>
<em> },</em>
<em> "userImageStorageContainerName": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "This is the name of the container in your storage account"</em>
<em> }</em>
<em> },</em>
<em> "userImageVhdName": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "This is the name of the your customized VHD"</em>
<em> }</em>
<em> },</em>
<em> "adminUserName": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "UserName for the Virtual Machine"</em>
<em> }</em>
<em> },</em>
<em> "adminPassword": {</em>
<em> "type": "securestring",</em>
<em> "metadata": {</em>
<em> "description": "Password for the Virtual Machine"</em>
<em> }</em>
<em> },</em>
<em> "osType": {</em>
<em> "type": "string",</em>
<em> "allowedValues": [</em>
<em> "windows",</em>
<em> "linux"</em>
<em> ],</em>
<em> "metadata": {</em>
<em> "description": "This is the OS that your VM will be running"</em>
<em> }</em>
<em> },</em>
<em> "vmSize": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "This is the size of your VM"</em>
<em> }</em>
<em> },</em>
<em> "vmNameBase": {</em>
<em> "type": "string",</em>
<em> "metadata": {</em>
<em> "description": "This is the size of your VM"</em>
<em> }</em>
<em> },</em>
<em> "vmCount":{</em>
<em> "type": "int",</em>
<em> "defaultValue": 1,</em>
<em> "metadata": {</em>
<em> "description": "The number of VMs to build."</em>
<em> }</em>
<em> }</em>
<em> },</em>
<em> "variables": {</em>
<em> "location": "[resourceGroup().location]",</em>
<em> "virtualNetworkName": "VNetName",</em>
<em> "addressPrefix": "10.6.0.0/16",</em>
<em> "subnet1Name": "default",</em>
<em> "subnet1Prefix": "10.6.0.0/24",</em>
<em> "publicIPAddressType": "Dynamic",</em>
<em> "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",</em>
<em> "subnet1Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",</em>
<em> "userImageName": "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]"</em>
<em> },</em>
<em> "resources": [</em>
<em> {</em>
<em> "apiVersion": "2015-05-01-preview",</em>
<em> "type": "Microsoft.Network/publicIPAddresses",</em>
<em> "name": "[concat(parameters('vmNameBase'),copyIndex(),'-PublicIP')]",</em>
<em> "copy": { </em>
<em> "name": "publicIPAddressCopy", </em>
<em> "count": "[parameters('vmCount')]" </em>
<em> },</em>
<em> "location": "[variables('location')]",</em>
<em> "properties": {</em>
<em> "publicIPAllocationMethod": "[variables('publicIPAddressType')]",</em>
<em> "dnsSettings": {</em>
<em> "domainNameLabel": "[concat(parameters('vmNameBase'),copyIndex())]"</em>
<em> }</em>
<em> }</em>
<em> },</em>
<em> {</em>
<em> "apiVersion": "2015-05-01-preview",</em>
<em> "type": "Microsoft.Network/networkInterfaces",</em>
<em> "name": "[concat(parameters('vmNameBase'),copyIndex(),'-NIC')]",</em>
<em> "location": "[variables('location')]",</em>
<em> "copy": { </em>
<em> "name": "networkInterfacesCopy", </em>
<em> "count": "[parameters('vmCount')]" </em>
<em> },</em>
<em> "dependsOn": [</em>
<em> "[concat('Microsoft.Network/publicIPAddresses/', parameters('vmNameBase'),copyIndex(),'-PublicIP')]"</em>
<em> ],</em>
<em> "properties": {</em>
<em> "ipConfigurations": [</em>
<em> {</em>
<em> "name": "ipconfig1",</em>
<em> "properties": {</em>
<em> "privateIPAllocationMethod": "Dynamic",</em>
<em> "publicIPAddress": {</em>
<em> "id": "[resourceId('Microsoft.Network/publicIPAddresses/',concat(parameters('vmNameBase'),copyIndex(),'-PublicIP'))]"</em>
<em> },</em>
<em> "subnet": {</em>
<em> "id": "[variables('subnet1Ref')]"</em>
<em> }</em>
<em> }</em>
<em> }</em>
<em> ]</em>
<em> }</em>
<em> },</em>
<em> {</em>
<em> "apiVersion": "2015-06-15",</em>
<em> "type": "Microsoft.Compute/virtualMachines",</em>
<em> "name": "[concat(parameters('vmNameBase'),copyIndex())]",</em>
<em> "copy": { </em>
<em> "name": "vmCopy", </em>
<em> "count": "[parameters('vmCount')]" </em>
<em> },</em>
<em> "location": "[variables('location')]",</em>
<em> "dependsOn": [</em>
<em> "[concat('Microsoft.Network/networkInterfaces/',parameters('vmNameBase'),copyIndex(),'-NIC')]",</em>
<em> "[concat('Microsoft.Network/publicIPAddresses/', parameters('vmNameBase'),copyIndex(),'-PublicIP')]"</em></h5>
<h5><em>],</em>
<em> "properties": {</em>
<em> "hardwareProfile": {</em>
<em> "vmSize": "[parameters('vmSize')]"</em>
<em> },</em>
<em> "osProfile": {</em>
<em> "computername": "[concat(parameters('vmNameBase'),copyIndex())]",</em>
<em> "adminUsername": "[parameters('adminUsername')]",</em>
<em> "adminPassword": "[parameters('adminPassword')]"</em>
<em> },</em>
<em> "storageProfile": {</em>
<em> "osDisk": {</em>
<em> "name": "[concat(parameters('vmNameBase'),copyIndex(),'-osDisk')]",</em>
<em> "osType": "[parameters('osType')]",</em>
<em> "caching": "ReadWrite",</em>
<em> "createOption": "FromImage",</em>
<em> "image": {</em>
<em> "uri": "[variables('userImageName')]"</em>
<em> },</em>
<em> "vhd": {</em>
<em> "uri": "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/vhds/',parameters('vmNameBase'), copyIndex(),'-osDisk.vhd')]"</em>
<em> }</em>
<em> }</em>
<em> },</em>
<em> "networkProfile": {</em>
<em> "name": "[concat(parameters('vmNameBase'),copyIndex(),'-networkProfile')]",</em>
<em> "networkInterfaces": [</em>
<em> {</em>
<em> "id": "[resourceId('Microsoft.Network/networkInterfaces/',concat(parameters('vmNameBase'),copyIndex(),'-NIC'))]"</em>
<em> }</em>
<em> ]</em>
<em> },</em>
<em> "diagnosticsProfile": {</em>

<em> "bootDiagnostics": {</em>
<em> "enabled": "true",</em>
<em> "storageUri": "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net')]"</em>
<em> }</em>
<em> }</em>
<em> }</em>
<em> }</em>
<em> ]</em>
<em>}</em></h5>
<h5>-------------------------------------------------------</h5>
The "copyIndex()" command is what tells the ARM engine to use the value from the loop.   Using "DependsOn" with this, means that Computer1 will depend upong Computer1-NIC and Computer1-PublicIP, so nothing will be built if the other parts aren't ready for it.

This template is setup to be used with a user image, something custom that I've put up there that's already sysprepped and ready-to-go.  I haven't yet made this add the resources for the extensions or gotten it to join the domain after being built, but at least I have the VMs running now.
