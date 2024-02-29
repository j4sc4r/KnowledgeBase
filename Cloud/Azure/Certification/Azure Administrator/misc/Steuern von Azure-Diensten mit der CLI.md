# Steuern von Azure-Diensten mit der CLI

- Finden von Befehlen 
```bash
#Befehle mit zusammenhang suchen
az find blob

or 

#Befehle die der CLI-Befehlsgruppe gehoeren
az find "az vm"

or

#Befehle die Parameter oder unterbefehle sind 
az find "az vm create"

or 

#Befehl Informationen zum Befehl
az storage blob --help
```

## Erstellen einer Azure Resource

- Grundbefehle
```bash
#Login to Azure
az login

# create resource group
az group create -n <name> -l <location>

# check if creation successfully
az group list

or 

az group list --output table
```


### Uebungserstellung einer Azure-Website

```bash
#create variables (optimal)
export RESOURCE_GROUP=<resource group name>
export AZURE_REGION=<region>
export AZURE_APP_PLAN=popupappplan-$RANDOM
export AZURE_WEB_APP=popupwebapp-$RANDOM

#show resource group, second is with filter
az group list --output table
az group list --query "[?name == '<resource group name']"

# create App Service-Plan
az appservice plan create 
-n $AZURE_APP_PLAN 
-g $RESOURCE_GROUP 
-l $AZURE_REGION 
--sku FREE

# check if creation successfully
az appservice plan list --output table

# create Webapp
az webapp create 
-n $AZURE_WEB_APP 
-g $RESOURCE_GROUP 
--plan $AZURE_APP_PLAN

# check if creation successfully
az webapp list --output table

# add content to the site via github
az webapp deployment source config 
-n $AZURE_WEB_APP 
-g $RESOURCE_GROUP 
--repo-url "https://github.com/Azure-Samples/php-docs-hello-world" 
--branch master
--manual-integration
```