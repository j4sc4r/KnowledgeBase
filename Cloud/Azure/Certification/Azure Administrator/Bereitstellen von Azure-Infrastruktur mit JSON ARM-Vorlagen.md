# Bereitstellen von Azure-Infrastruktur mit JSON ARM-Vorlagen

## Vorteile von Infrastructure-as-Code (IaC)

- Konsistente Konfigurationen
- Verbesserte Skalierbarkeit
- Schnellere Bereitstellungen
- Bessere Nachverfolgbarkeit

## Vorteile von ARM-Vorlagen

- Verwendung von IaC moeglich
- sind idempotent, d. h., dass Sie dieselbe Vorlage mehrmals bereitstellen können, wobei Sie dann dieselben Ressourcentypen im selben Zustand erhalten
- Resource Manager orchestriert die Bereitstellung der Ressourcen
- dieser achtet auf die richtige Reihenfolge des Deployments und evtl. auf parallelisierung der Prozesse
- überprüft die Vorlage vor dem Start der Bereitstellung, um sicherzustellen, dass die Bereitstellung erfolgreich sein wird
- ARM-Vorlagen in kleinere, wiederverwendbare Komponenten aufteilen
- Azure-Portal können Sie Ihren Bereitstellungsverlauf überprüfen
- koennen auch in CI/CD Pipelines integriert werden

![[Azure_Resource_Manager.png]]


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

## Bereitstellen einer ARM-Vorlage in Azure

- Bereitstellen als lokale Vorlage
- Bereitstellen als verknüpfte Vorlage
- Bereitstellen in einer Continuous Deployment-Pipeline
- muessen Ressourcenanbieter und dessen zugehörige Ressourcentypen kennen
- Syntax für diese Kombination hat die Form {resource-provider}/{resource-type}
- Weitere Informationen finden Sie unter [Definieren von Ressourcen in Azure Resource Manager-Vorlagen](https://learn.microsoft.com/de-de/azure/templates)

### Erstellen einer ARM-Vorlage

- Oeffnen von Microsoft Studio 
- erstellen des ARM-Templates
- Mit VSCode addon `arm!`

![[Azure_ARM_Temp.png]]

- Deployen des Templates 
```bash
az deployment group create -n <name> --template-file <path to file>
```

## ARM-Vorlagenparameter

- in `parameters` der Vorlage wird angegeben welche Werte Sie beim Bereitstellen der Ressourcen eingeben können
- beschraenkung auf 256 Parameter

Folgende Eigenschaften sind fuer Parameter verfuegbar:

```json
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [
      "<array-of-allowed-values>"
    ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the-parameter>"
    }
  }
}
```

Zulaessige Parametertypen sind: 

- string
- secureString
- integers
- boolean
- object
- secureObject
- array

Beispiel einer Verwendung der ARM-Vorlage mit Parameter:

- `parameters` for SKU 
```json
"parameters": {
  "storageAccountType": {
    "type": "string",
    "defaultValue": "Standard_LRS",
    "allowedValues": [
      "Standard_LRS",
      "Standard_GRS",
      "Standard_ZRS",
      "Premium_LRS"
    ],
    "metadata": {
      "description": "Storage Account type"
    }
  }
}
```

- `parameters` added in `resources`
- syntax: `[parameters('name of the parameter')]`
```json
"resources": [
  {
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2019-04-01",
    "name": "learntemplatestorage123",
    "location": "[resourceGroup().location]",
    "sku": {
      "name": "[parameters('storageAccountType')]"
    },
    "kind": "StorageV2",
    "properties": {
      "supportsHttpsTrafficOnly": true
    }
  }
]
```

- Bei Bereitstellung der Vorlage 
```bash
az deployment group create \
  --name testdeployment1 \
  --template-file $templateFile \
  --parameters storageAccountType=Standard_LRS
```

## ARM-Vorlagenausgaben

- koennen unter dem punkt `outputs` Werte angegeben werden die nach erfolgreicher Bereitstellung zurueckgegeben werden 

```json
"outputs": {
  "<output-name>": {
    "condition": "<boolean-value-whether-to-output-value>",
    "type": "<type-of-output-value>",
    "value": "<output-value-expression>",
    "copy": {
      "count": <number-of-iterations>,
      "input": <values-for-the-variable>
    }
  }
}
```

| Element     | Beschreibung                                                                                                                                                                                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| output-name | Es muss sich um einen gültigen JavaScript-Bezeichner handeln.                                                                                                                                                                                                                                     |
| condition   | (Optional) Ein boolescher Wert, der angibt, ob dieser Ausgabewert zurückgegeben wird. Bei „true“ wird der Wert in die Ausgabe für die Bereitstellung aufgenommen. Bei „false“ wird der Ausgabewert für diese Bereitstellung übersprungen. Wenn keine Angabe erfolgt, ist der Standardwert „true“. |
| type        | Der Typ des Ausgabewerts.                                                                                                                                                                                                                                                                         |
| value       | (Optional) Ein Vorlagensprachausdruck, der ausgewertet und als Ausgabewert zurückgegeben wird.                                                                                                                                                                                                    |
| copy        | (Optional) „copy“ wird zum Zurückgeben von mehr als einem Wert für eine Ausgabe verwendet.                                                                                                                                                                                                        |

### Verwenden von Ausgaben in einer ARM-Vorlage

Beispiel:
```json
"outputs": {
  "storageEndpoint": {
    "type": "object",
    "value": "[reference('<templatename>').primaryEndpoints]"
  }
}
```
- `reference` ruft den Laufzeitzustand des Speicherkontos ab 

## Uebung zur Bereitstellung von ARM-Vorlagen mit Parametern und Ausgaben

- add in VSCode under parameters `par` to add a new parameter
- add the parameter to the resource
```json 
"resources": [
    {
      "name": "[parameters('storageName')]",         <---- HERE
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-06-01",
      "tags": {
        "displayName": "[parameters('storageName')]" <---- HERE
      },
      "location": "[resourceGroup().location]",
      "kind": "StorageV2",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      }
    }
  ],
```

- deployment des neuen Templates
```bash
az deployment group create \
  --name $DeploymentName \
  --template-file $templateFile \
  --parameters storageName={your-unique-name} <additonal parameters>
```

- hinzufuegen eines outputs
- klick in die `"outputs":{},` Klammern
- Enter + "out" um neue Liste zu erstellen
```json
"outputs": {
  "output1": {
    "type": "string",
    "value": "value"
  }
```

- aender diese sodass die Endpunktendaten des Storages ausgegeben werden 
```json
"outputs": {
  "storageEndpoint": {
    "type": "object",
    "value": "[reference(parameters('storageName')).primaryEndpoints]"
  }
```

-deploy 
```bash
az deployment group create \
  --name $DeploymentName \
  --template-file $templateFile \
  --parameters storageSKU=Standard_LRS storageName={your-unique-name}
```

- Output

![[Azure_Storage_Endpoints.png]]