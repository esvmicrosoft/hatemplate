# hatemplate

Deploy an HA SLES15 cluster template 


The HAtemp.json file is an annotated version of the template but it does not pass syntax checks for a JSON document, the HAtemp.jsonc is an annotated version of the template and can be deployed using the following commands.

```
export rg=clusterrg
export location=eastus

ssh-keygen -t rsa -b 2048 -N"" -f azureuser_key
privkey=$(cat azureuser_key)
pubkey=$(cat azureuser_key.pub)
myip=$(curl ident.me 2>/dev/null)

az group create --name $rg --location "$location"
az deployment group create --name blanktemplate --resource-group $rg --template-file HAtemp.jsonc \
     --parameters parameters.json --parameters privkey="$privkey" --parameters pubkey="$pubkey"   \
     --parameters myipaddress=${myip}
```
