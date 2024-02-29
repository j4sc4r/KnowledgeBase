# Azure ARM-Templates

## ARM-Vorlagendateistruktur

| Element        | Beschreibung                                                                                                                                                                                                                                                                                                                                                                        |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| schema         | Ein erforderlicher Abschnitt, der den Speicherort der JSON-Schemadatei definiert, in der die Struktur von JSON-Daten beschrieben wird. Die von Ihnen verwendete Versionsnummer hängt vom Umfang der Bereitstellung und vom JSON-Editor ab.                                                                                                                                          |
| contentVersion | Ein erforderlicher Abschnitt, der die Version Ihrer Vorlage definiert (z. B. 1.0.0.0). Mit diesem Wert können Sie signifikante Änderungen an Ihrer Vorlage dokumentieren, um sicherzustellen, dass Sie die richtige Vorlage bereitstellen.                                                                                                                                          |
| apiProfile     | Ein optionaler Abschnitt, der eine Sammlung von API-Versionen für Ressourcentypen definiert. Sie können diesen Wert verwenden, um zu vermeiden, dass Sie API-Versionen für jede Ressource in der Vorlage angeben müssen.                                                                                                                                                            |
| parameters     | Ein optionaler Abschnitt, in dem Sie Werte definieren, die während der Bereitstellung angegeben werden. Diese Werte können über eine Parameterdatei, über Befehlszeilenparameter oder im Azure-Portal bereitgestellt werden.                                                                                                                                                        |
| variables      | Ein optionaler Abschnitt, in dem Sie Werte definieren, die verwendet werden, um Vorlagensprachausdrücke zu vereinfachen.                                                                                                                                                                                                                                                            |
| functions      | Ein optionaler Abschnitt, in dem Sie [benutzerdefinierten Funktionen](https://learn.microsoft.com/de-de/azure/azure-resource-manager/templates/template-user-defined-functions) (UDF) definieren können, die in der Vorlage verfügbar sind. Benutzerdefinierte Funktionen können Ihre Vorlage vereinfachen, wenn komplizierte Ausdrücke wiederholt in der Vorlage verwendet werden. |
| resources      | Ein erforderlicher Abschnitt, der die tatsächlichen Elemente, die Sie in einer Ressourcengruppe oder einem Abonnement bereitstellen bzw. aktualisieren möchten, definiert.                                                                                                                                                                                                          |
| output         | Ein optionaler Abschnitt, in dem Sie die Werte angeben, die am Ende der Bereitstellung zurückgegeben werden.                                                                                                                                                                                                                                                                        |

## Elemente im Ueberblick

Standard JSON Struktur fuer ein ARM-Template:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {}, <---- Parameter input
    "functions": [],
    "variables": {},
    "resources": [],  <---- Resource input
    "outputs": {}
}
```


### Resources 

- hier werden die einzelnen resourcen eingetragen die Bereitgetellt werden sollen

**Beispiel VM**
Zu einer VM gehoeren zusaetzlich die OsDisk, das Network Interface und die VM selber
```json
# Network interface
{

            "name": "[concat(parameters('vmName'), copyIndex(), '-nic')]",
            "type": "Microsoft.Network/networkInterfaces",
            "apiVersion": "2023-04-01",
            "location": "germanywestcentral",
            "dependsOn": [
                "[resourceId('Microsoft.Network/virtualNetworks', concat(parameters('vmName'), '-vn'))]"
            ],
            "copy":{
                "name": "nicCopy",
                "count": "[parameters('count')]"
            },
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipConfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', concat(parameters('vmName'), '-vn'), concat(parameters('vmName'), '-sub'))]"

                            }

                        }

                    }

                ]

            }

        },
# VM
{
            "name": "[concat(parameters('vmName'), copyIndex())]",
            "type": "Microsoft.Compute/virtualMachines",
            "apiVersion": "2023-03-01",
            "location": "germanywestcentral",
            "dependsOn": [
                "nicCopy"
            ],
            "copy":{
                "name": "vmCopy",
                "count": "[parameters('count')]"
            },
            "properties": {
                "hardwareProfile": {
                    "vmSize": "[parameters('MachineSKU')]"
                },
                "osProfile": {
                    "computerName": "[concat(parameters('vmName'), copyIndex())]",
                    "adminUsername": "[parameters('UserName')]",
                    "adminPassword": "[parameters('UserPassword')]"
                },
                "storageProfile": {
                    "imageReference": {
                        "publisher": "Canonical",
                        "offer": "UbuntuServer",
                        "sku": "16.04-LTS",
                        "version": "latest"
                    },
# OS-Disk
                    "osDisk": {
                        "name": "[concat(parameters('vmName'), copyIndex(), '-disk')]",
                        "caching": "ReadWrite",
                        "createOption": "FromImage"
                    }
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(parameters('vmName'), copyIndex(), '-nic'))]"
                        }
                    ]
                }
            }
        }
```

**Beispiel Storage**
Hier wird ein Storage account + FileShare bereitgestellt
```json
# Storage account
"resources": [
        {
            "name": "[parameters('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-01-01",
            "location": "[resourceGroup().location]",
            "kind": "StorageV2",
            "sku": {
                "name": "Standard_LRS",
                "tier": "Standard"
            }
        },
# File share        
        {
            "type": "Microsoft.Storage/storageAccounts/fileServices/shares",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('storageAccountName'), '/default/', parameters('fileShareName'))]",
            "dependsOn": [
                "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]"
            ],
            "properties": {
                "shareQuota": 5
            }
        }
    ],
```

### Parameters

- hier werden parameter hinzugefuegt, die waehrend der Template bereitstellung angegeben werden

**Bespiel Name von einem Storage account**

```json
    "parameters": {
# Storage account name 
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of the storage account"
            }
        },
# File share name         
        "FileShareName": {
            "type": "string",
            "metadata": {
                "description": "Name of file share"
            }
        }
    },
```

**Eingebaut in die Resource**

```json
"resources": [
        {
            "name": "[parameters('storageAccountName')]", <---- Storage name
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-01-01",
            "location": "[resourceGroup().location]",
            "kind": "StorageV2",
            "sku": {
                "name": "Standard_LRS",
                "tier": "Standard"
            }
        },
# File share        
        {
            "type": "Microsoft.Storage/storageAccounts/fileServices/shares",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('storageAccountName'), '/default/', parameters('fileShareName'))]",  <---- File share name mit extra beschriftung
            "dependsOn": [
                "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]"  <---- storageAccountName
            ],
            "properties": {
                "shareQuota": 5
            }
        }
    ],
```

### Variables 

### Functions

### Deployment of the Template

**Um ein Template in Azure zu deployen**

```bash
# login Azure account
az login

# show available subscription and choose Azure subscription
az account show
az account set --subscription "<name>"

# deploy in resource group
az deployment group create -n <templatename> -g <resource group> -f <path to template> --parameters <parameters eg. FileShareName=TestName> 
```