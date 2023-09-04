### Login on Azure
az login

### General Parameters
rg=rg-virtualnetwork
local=brazilsouth

### Parameters Virtual Network
vnetbr=vnet-brazilsouth
vnetus=vnet=eastus2

###  Create Resource Group
az group create -n $rg -l $local

###  Create Virtual Network 
az network vnet create -g $rg -n $vnetbr --address-prefixes 10.0.0.0/16 -l $local

###  Create Virutal Network and Subnet
az network vnet create -g $rg $vnetus --address-prefixes 10.100.0.0/16 --subnet-name snet-default --subnet-prefixes 10.100.1.0/24 -l eastus2

### List Virtual Network
az network vnet list
az network vnet list -g $rg -o yaml

### List Virtual Networks on specific address
az network vnet list --query "[?contains(addressSpace.addressPrefixes, '10.100.0.0/16')]" -o table

### Show Details Vnet
az network vnet show -g $rg -n $vnetbr -o yaml

### Updade Vnet prefix
az network vnet update --address-prefixes 10.200.0.0/16 -n $vnetbr -g $rg

### List IPs Availables on Vnet
az network vnet list-available-ips -g $rg -n $vnetbr

### Create Subnets on Vnet
az network vnet subnet create -g $ $rg --vnet-name $vnetbr -n snet1 --address-prefixes 10.100.1.0.24
az network vnet subnet create -g $ $rg --vnet-name $vnetbr -n snet2 --address-prefixes 10.100.2.0.24

### List Subnets on Vnet
az network vnet subnet-list -g $rg --vnet-name $vnet $vnetbr -o table

### Show Subnet Details
az network vnet subnet show -g $rg --vnet-name $vnetbr -n snet1 -o yaml

### Show IPs Availables on Subnet
az network vnet subnet list-available-ips -g $rg --vnet-name $vnetbr -n snet1

### Update Subnet Addres Prefixes
az network vnet subnet update -n snet2 --vnet-name $vnetbr -g $rg --address-prefixes "10.100.3.0/24"

### Delete Subnet
az network vnet subnet delete -n snet2 --vnet-name $vnetbr

### Delete Virtual Network
az network vnet delete -n $vnetbr-g $rg

### Delete Resource Group
az group delete -n $rg -y