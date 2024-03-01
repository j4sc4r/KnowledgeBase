# Konfigurieren von Azure-Resources mit ARM-Vorlagen

## Vorteile 

- Vorlagen sorgen fuer mehr Konsistenz
	- bieten eine gemeinsame Sprache zur Beschreibung Ihrer Bereitstellungen
	- unabhaenig vom Tool, Struktur, Format und Ausdrücke innerhalb der Vorlage bleiben unverändert
- Helfen beim Umsetzen komplexer Bereitstellungen
	- ermöglichen die Bereitstellung mehrerer Ressourcen in der richtigen Reihenfolge
- Reduziert manuelle, fehleranfaellige Aufgaben
	- manuelle Erstellen und Verbinden von Ressourcen kann zeitaufwendig und fehleranfällig sein
	- stellt sicher, dass die Bereitstellung jedes Mal auf die gleiche Weise erfolgt
- Vorlagen bestehen aus Code
- Vorlagen foerdern die Wiederverwendung
	- kann Parameter enthalten, die beim Ausführen der Vorlage ausgefüllt werden
	- kann einen Benutzernamen oder ein Kennwort, einen Domänennamen usw. definieren
	- Über Vorlagenparameter können mehrere Versionen der Infrastruktur erstellt werden, z. B. Staging und Produktion, aber trotzdem genau die gleiche Vorlage verwenden
- Vorlagen sind Verknuepfbar
	- können Resource Manager-Vorlagen miteinander verknüpfen
	- modularere Gestaltung 
	- können kleinere Vorlagen schreiben, die jeweils einen Teil einer Lösung definieren, und diese dann zu einem Gesamtsystem kombinieren
- Vorlagen vereinfachen die Orchestrierung 
	- müssen nur die Vorlage bereitstellen, um alle Ihre Ressourcen bereitzustellen

## ARM-Vorlagenschema

**Beispiel JSON:**
```json
{
    "$schema": "http://schema.management.​azure.com/schemas/2019-04-01/deploymentTemplate.json#",​
    "contentVersion": "",​
    "parameters": {},​
    "variables": {},​
    "functions": [],​
    "resources": [],​
    "outputs": {}​
}
```

| Elementname    | Erforderlich | Beschreibung                                                                                                                                                                                                                                                           |
| -------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $schema        | Ja           | Speicherort der JSON-Schemadatei, die die Version der Vorlagensprache beschreibt. Verwenden Sie die im vorherigen Beispiel gezeigte URL.                                                                                                                               |
| contentVersion | Ja           | Version der Vorlage (z. B. 1.0.0.0). Sie können einen beliebigen Wert für dieses Element resources. Mit diesem Wert können Sie wichtige Änderungen in der Vorlage dokumentieren. Mit diesem Wert kann sichergestellt werden, dass die richtige Vorlage verwendet wird. |
| parameters     | Nein         | Werte, die bei der Bereitstellung angegeben werden, um die Bereitstellung der Ressourcen anpassen.                                                                                                                                                                     |
| variables      | Nein         | Werte, die als JSON-Fragmente in der Vorlage verwendet werden, um Vorlagensprachausdrücke zu vereinfachen.                                                                                                                                                             |
| functions      | Nein         | Benutzerdefinierte Funktionen, die in der Vorlage verfügbar sind.                                                                                                                                                                                                      |
| resources      | Ja           | Ressourcentypen, die in einer Ressourcengruppe bereitgestellt oder aktualisiert werden.                                                                                                                                                                                |
| outputs        | Nein         | Werte, die nach der Bereitstellung zurückgegeben werden.                                                                                                                                                                                                               | 

**Beispiel des parameter Elements in JSON-Dateien:**

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
        "description": "<description-of-the parameter>"
        }
    }
}
```

```json
"parameters": {
  "adminUsername": {
    "type": "string",
    "metadata": {
      "description": "Username for the Virtual Machine."
    }
  },
  "adminPassword": {
    "type": "securestring",
    "metadata": {
      "description": "Password for the Virtual Machine."
    }
  }
}
```

### Bicep-Vorlagen

![[Azure_Bicep.png]]

#### Verbesserungen von Bicep gegenueber der ARM-Templates

- Einfachere Syntax
- Module
	- können komplexe Vorlagenbereitstellungen in kleinere Moduldateien aufteilen
	- koennen in einer Hauptvorlage benutzt werden
	- ermöglichen eine einfachere Verwaltung und bessere Wiederverwendbarkeit
- Automatische Verwaltung von Abhaengigkeiten
	- Bicep erkennt Abhängigkeiten zwischen Ressourcen automatisch
	- Prozess nimmt Ihnen einen Teil der Arbeit bei der Erstellung von Vorlagen ab
- Typvalidierung und IntelliSense
	- Bicep-Erweiterung für Visual Studio Code bietet eine umfassende Validierung und IntelliSense für alle API-Definitionen von Azure-Ressourcentypen

### Azure-Schnellstartvorlagen

- werden von der Azure Community zur verfuegung gestellt
- Die Datei „README.md“ enthält eine Übersicht über die Funktion der Vorlage
- In der Datei „azuredeploy.json“ werden die bereitgestellten Ressourcen definiert
- Die Datei „azuredeploy.parameters.json“ stellt die Werte für die Vorlage bereit

### Review an ARM template 

- In der resource group unter settings --> deployment --> template
- searchbar: Deploy custom template

