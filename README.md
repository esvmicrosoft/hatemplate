# hatemplate

Deploy an HA Suse cluster template 


The HAtemp.json file is an annotated version of the template but it does not pass syntax checks for a JSON document, in order to make use of it execute the following series of commands:

```
export rg=clusterrg
export location=eastus

ssh-keygen -t rsa -b 2048 -N"" -f azureuser_key
priv_key=$(cat azureuser_key)
pub_key=$(cat azureuser_key.pub)

az group create --name $rg --location "$location"
az deployment group create --name blanktemplate --resource-group $rg --template-file HAtemp.jsonc \
     --parameters parameters.json --parameters privkey="$priv_key" --parameters pubkey="$pubkey"
```
