# AZ - 104 - Deploy Compute resources

# VM - Groesse (VM - Size)

| Klassifizierung            | Beschreibung                                                       | Zweck                                                          |
| -------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------- |
| Allgemeiner Zweck          | Ausgewogenes Verhaeltnis CPU und RAM                               | kleine Webserver, Tests und Entwicklung, kleine Datenbanken    |
| Fuer Compute optimiert     | Hohes Verhaeltnis von CPU zu RAM                                   | Netzwerkgeraete, Anwendungsserver, Batchprozesse               |
| Arbeitsspeicherorientiert  | Hohes Verhaeltnis von RAM zu CPU                                   | In-Memory Analysen, relationale Datenbanken, Caches            |
| Speicheroptimiert          | hoher Datentraegerdurchsatz mit hoher E/A-Leistung                 | Big Data, SQL-, NoSQL DBs, Data Warehousing                    |
| GPU                        | spezialisert auf Grafikrendering und intensiver Videobearbeitung   | Modelltraining, Deep-Learning                                  |
| High Performance Computing | HPC bietet leistungsstaerkste CPUs mit schnellem Netzwerkdurchsatz | Netzwerke mit hohem Datenverkehr, Workloads mit hoher Leistung |

# VM Verfuegbarkeit

- Azure updatet oder patch nicht automatisch das VM Betriebssystem

## Verfuegbarkeitsgruppen

- logische Gruppe von VMs
- keine gleichzeitige Aktualisierung während des Host-Upgrades im Rechenzentrum
- gewährleistet die Bereitstellung
- sollten identische Funktionen und Software haben
- Azure stellt sicher, dass sie über mehrere physische Server, Speicher und Switches laufen
- im Falle eines Ausfalls ist nur eine Untergruppe von VMs betroffen

## Update- und Fehlerdomains

### Updatedomain
- eine Gruppe von Knoten, die gemeinsam geupgraded werden
- können gleichzeitig neu gebootet werden
- Standard: 5

### Fehlerdomains

- VM-Gruppe, die einen gemeinsamen Fehlerpunkt (single point of failure) hat.
- Beispiel: Server-Rack

## Verfuegbarkeitszonen

- eindeutige physische Standorte innerhalb der Region
- bestehend aus 1 oder mehreren Rechenzentren

## Azure Virtual Machine Scale Sets

- setzt eine Reihe **identischer** vms ein
- autoscaled nach Auslastung
- manueller oder automatischer Prozess des hinzufuegen bzw. entfernen der VM-Instanzen
- bis zu 1000 vm-Instanzen

# Azure App Service Plaene

- definiert eine Reihe von Rechenressourcen für die Ausführung einer Webanwendung
- kann eine oder mehrere Anwendungen enthalten
- jeder App-Plan definiert:
	- Region
	- Anzahl der VM-Instanzen
	- Größe der VM-Instanzen

## Free and Shared Tiers

In den Tiers Free und Shared erhält eine Anwendung CPU-Minuten auf einer gemeinsam genutzten VM-Instanz und kann nicht skaliert werden.

## Basic, Standard, Premium, Isolated Tiers

![[Azure_Service_Plan.png]]

# Azure App Service

- Im Serviceplan ausgeführte Anwendungen  
- mehrere Anwendungen im gleichen Plan teilen sich die gleichen VMs
- mehrere Deployment Slots laufen auch auf denselben VMs  
- Der Plan ist die Skalierungseinheit 
	- Autoscaling skaliert alle Anwendungen im Plan  
- Da Anwendungen dieselben Ressourcen nutzen, sollten Sie vorsichtig sein, wenn Sie Ihrem Plan weitere Anwendungen hinzufügen.  
	- Verstehen Sie die Kapazität des Plans  
	- Verstehen Sie die Last der neuen Anwendung

## Bereitstellungs Slots

- Live App mit eigenem Hostnamen

Ein Deployment Slot ist eine Instanz eines App Service, die auf demselben App Service Plan läuft.
Sie muss ausgetauscht werden, um die Instanz in der Produktion einzusetzen. Dies ermöglicht eine Bereitstellung ohne Ausfallzeiten.

## App Service Sicherheit

- Das Sicherheitsmodul für die Authentifizierung und Autorisierung in Azure App Service wird in derselben Umgebung wie Ihr Anwendungscode ausgeführt, allerdings separat.
- Das Sicherheitsmodul wird mithilfe von App-Einstellungen konfiguriert. Weder SDKs noch bestimmte Sprachen oder Änderungen am Anwendungscode sind erforderlich.
- Wenn Sie das Sicherheitsmodul aktivieren, durchläuft jede eingehende HTTP-Anforderung das Modul, bevor es vom Anwendungscode verarbeitet wird.
- Das Sicherheitsmodul übernimmt mehrere Aufgaben für Ihre App:
    - Authentifizierung von Benutzer*innen mit dem angegebenen Anbieter
    - Überprüfen, Speichern und Aktualisieren von Token
    - Verwalten der authentifizierten Sitzung
    - Einfügen von Identitätsinformationen in Anforderungsheader

