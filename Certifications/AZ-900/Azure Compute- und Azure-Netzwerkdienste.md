# Azure Compute- und Azure-Netzwerkdienste

## Azure-VMs

VMs stellen IaaS (Infrastructure-as-a-Service) in Form eines virtualisierten Servers zur Verfügung.

VMs sind ideal bei folgenden Szenarien:
- Vollständige Kontrolle über das Betriebssystem
- Die Möglichkeit, benutzerdefinierte Software auszuführen
- Die Möglichkeit, benutzerdefinierte Hostingkonfigurationen zu verwenden

Bereits erstellte Images koennen benutzt werden um spezifische Software noch schneller auf einer VM bereitzustellen.

### Skalieren der Azure-VMs

- Einzelbereitstellung fuer Test- und Entwicklungsaufgaben
- gruppierte Bereitstellung um Hochverfügbarkeit, Skalierbarkeit und Redundanz zu gewährleisten
- Azure kann Gruppierung von VMs mit Features wie Skalierungsgruppen und Verfügbarkeitsgruppen verwalten

#### VM-Skalierungsgruppen

- identische VMs koennen mit Load Balancing erstellt und verwaltet werden
- koennen eine große Anzahl von VMs innerhalb weniger Minuten zentral verwalten, konfigurieren und aktualisieren
- VM-Instanzen koennen nach vordefinierten Zeitplan automatisch erhöht oder verringert werden

#### VM-Verfuegbarkeitsgruppen

- Verschieben VM-Updates um bei Ausfall eines Netzwerkes/Stromausfall nicht alle VMs zu verlieren
- Stromversorung und Netzwerkverbindung ist unabhaengig konfiguriert

Erreicht wird das auf zwei Arten:
- Updatedomain
	- Gruppierung von VMs die gleichzeitig neu gestartet werden können
	- Gleichzeitiges Updaten und sicher sein, dass nur eine Gruppe in einer Updatedomäne gleichzeitig offline ist
	- Wenn Updategruppe den Updateprozess durchläuft, werden 30 Minuten Zeit für die Wiederherstellung gewährt, bevor die Wartung in der nächsten Updatedomäne gestartet wird
- Fehlerdomain
	- Gruppierung von VMs mit einer gemeinsamen Stromquelle und einem Netzwerkswitch
	- Standardmäßig werden VMs in einer Verfügbarkeitsgruppe auf bis zu drei Fehlerdomänen aufgeteilt
	- hilft beim Schutz vor einem physischen Stromversorgungs- oder Netzwerkfehler, da Ihre VMs sich in verschiedenen Fehlerdomänen befinden

Es fallen keine zusaetzlichen Kosten an, es werden nur die VM-Instanzen bezahlt.

### Wechsel von VMs in die Cloud

- Wechsel von on-premise VMs in die Cloud wird als "Lift and Shift" bezeichnet
- es kann ein Image des physischen Servers erstellt werden und dieses auf einer VM mit wenigen oder gar keinen Änderungen gehostet werden
- VMs muessen genauso wie ein physischer lokaler Server verwaltet werden

### VM-Ressourcen

- Größe (Zweck, Anzahl der Prozessorkerne und Menge von RAM)
- Speicherdatenträger (Festplatten, SSD-Laufwerke usw.)
- Netzwerk (virtuelles Netzwerk, öffentliche IP-Adresse und Portkonfiguration)

### Erstellen einer Azure-VM via Azure CLI

```bash
az vm create 
--resource-group "learn-a14654d1-5c80-4773-96ea-59bfa8faff91" 
--name my-vm 
--public-ip-sku Standard 
--image Ubuntu2204 
--admin-username azureuser 
--generate-ssh-keys
```

Um eine Extension der VM hinzuzufuegen:

```bash
az vm extension set 
--resource-group "learn-a14654d1-5c80-4773-96ea-59bfa8faff91" 
--vm-name my-vm 
--name customScript 
--publisher Microsoft.Azure.Extensions 
--version 2.1 
--settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' 
--protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```

- Verwendet die benutzerdefinierte Skripterweiterung, um ein Bash-Skript auf Ihrer VM auszuführen

### Azure Virtual Desktop

- ist ein in der Cloud ausgeführter Dienst für die Desktop- und Anwendungsvirtualisierung
- bietet zentralisierte Sicherheitsverwaltung für die Desktops von Benutzern mit Microsoft Entra ID
- mehrstufige Authentifizierung zum Sichern von Benutzeranmeldungen
- Datensicherheitserhoehung durch differenzierte und rollenbasierte Zugriffssteuerung der Benutzer
- Daten und Apps werden von Lokaler Hardware getrennt

## Azure-Container

Container sind eine gute Wahl, wenn Sie mehrere Instanzen einer Anwendung auf einer einzelnen Host-VM ausführen möchten

### Was sind Container


![[Azure_VMs.png]] ![[Azure_Containers.png]]

- sind eine Virtualisierungsumgebung
- können mehrere Container auf einem einzigen physischen oder virtuellen Host ausführen
- Das Container Betriebssystem wird nicht verwaltet
- sind schlank und so konzipiert, dass sie dynamisch erstellt, skaliert und beendet werden können
- stellen eine weniger aufwendige, agilere Methode dar als VMs
- sind so konzipiert, dass Sie bei Bedarf auf Änderungen reagieren können
- im Fall eines Absturzes oder einer Hardwareunterbrechung koennen sie schnell neu gestartet werden


### Azure Container Instances

- bietet die schnellste und einfachste Möglichkeit ohne VM-Verwaltungsaufwand, einen Container in Azure auszuführen
- Containerverwaltung notwendig
- ist ein PaaS-Angebot
- Container hochladen und dann durch den Dienst ausführen lassen

### Azure Container Apps

- ähnelt in vielerlei Hinsicht einer Containerinstanz
- Keine Containerverwaltung notwendig
- hat zusätzliche Vorteile, z. B. die Möglichkeit, Lastenausgleich und Skalierung zu integrieren

### Azure Kubernetes Service

- ist ein Containerorchestrierungsdienst
- Orchestrierungsdienst verwaltet den Lebenszyklus von Containern
- Wenn eine Containerflotte bereitgestellt wird, kann AKS die Flottenverwaltung einfacher und effizienter gestalten.

## Azure Functions

- ereignisgesteuerte, serverlose Computeoption, die keine Wartung von VMs oder Containern erfordert
- Funktion wird durch ein Ereignis ausgelöst, sodass keine Ressourcen bereitgestellt werden müssen, wenn keine Ereignisse vorhanden sind

Vorteile von Azure Functions:
- eignet sich ohne Infrastrukur aufwand, wenn nur der Code eines Dienstes ausgefuehrt werden soll
- wird verwendet, als Reaktion auf ein Ereignis z.B. REST Anfrage, einen Timer oder eine Nachricht von einem anderen Azure-Dienst
- wird automatisch nach Bedarf skaliert und ist somit eine gute Wahl, wenn der Bedarf variabel ist
- führt Ihren Code aus, wenn er ausgelöst wird, und hebt die Zuteilung von Ressourcen automatisch auf, wenn die jeweilige Funktion beendet wurde
- CPU-Berechnungszeit wird in Rechnung gestellt

## Azure App Service

- ermöglicht Ihnen das Erstellen und Hosten von Web-Apps, Hintergrundaufträgen, mobilen Back-Ends und RESTful-APIs
- bietet automatische Skalierung und hohe Verfügbarkeit
- unterstuetzt Windows und Linux
- ermöglicht automatisierte Bereitstellungen über GitHub, Azure DevOps oder ein beliebiges Git-Repository zur Unterstützung eines Continuous Deployment-Modells

### Typen von App-Diensten

- Web-Apps
- API-Apps
- WebJobs
- Mobile Apps

App Service übernimmt die meisten Infrastrukturentscheidungen z.B.:

- Funktionen zur Bereitstellung und Verwaltung sind in die Plattform integriert
- Endpunkte koennen gesichert werden
- Websites lassen sich schnell skalieren, um hohe Datenverkehrslasten zu bewaeltigen
- integrierte Load Balancing und Traffic Manager Funktionen ermoeglichen Hochverfuegbarkeit

## Azure-Netzwerke

Mit virtuellen Azure-Netzwerken und virtuellen Subnetzen können Azure-Ressourcen kommunizieren. 

Funktionen: 

- Isolation und Segmentierung 
- Internetkommunikation
- Kommunikation zwischen Azure-Ressourcen
- Kommunikation mit lokalen Ressourcen
- Weiterleitung von Netzwerkdatenverkehr 
- Verbindung virtueller Netzwerke

Azure unterstuetzt Oeffentlich und Private Endpunkte:

- Öffentliche Endpunkte haben eine öffentliche IP-Adresse, auf die von jedem Ort der Welt aus zugegriffen werden kann.
- Private Endpunkte sind in einem virtuellen Netzwerk enthalten und weisen eine private IP-Adresse im Adressraum des virtuellen Netzwerks auf.

### Isolation und Segmentierung

- Azure Virtual Network ermöglicht die Erstellung isolierter virtueller Netzwerke
- erstellter IP-Adressbereich des Virtual Networks kann nicht ueber das Internet geroutet werden
- IP Bereich kann in Subnetze unterteilt werden
- Integrierter Dienst zur Namensaufloesung

### Internetkommunikation

- Ressource benoetigt Public IP
- Ressource steht hinter einem Load Balancer

### Kommunikation zwischen Azure-Ressourcen

- Es koennen nicht nur VMs sondern jegliche Ressourcen in das Virtual Network eingefuegt werden
- Mithilfe von Dienstendpunkten können Sie eine Verbindung mit anderen Azure-Ressourcentypen herstellen
- Stellt optimale Sicherheit und Routing zwischen Ressourcen dar

### Kommunikation mit lokalen Ressourcen

- Moeglichkeit lokale Ressourcen mit dem Azure Abonnement zu verknuepfen
- Es kann ein Netzwerk erstellt werden was die Cloud und die Lokale Umgebung abdeckt

3 Mechanismen fuer die Herstellungen dieser Konnektivitaet: 

- Point-to-Site-VPN 
	- VPN besteht zwischen einem Computer außerhalb Ihrer Organisation zurück in das Unternehmensnetzwerk
	- Clientcomputer initiiert eine verschluesselte VPN-Verbindung
- Site-to-Site-VPN
	- verbinden des lokalen VPN-Geräts oder -Gateways mit dem Azure-VPN-Gateway in einem virtuellen Netzwerk
	- Verbindung ist verschlüsselt und internetbasiert
- Azure ExpressRoute
	- bietet dedizierte private Konnektivität mit Azure ohne eine Datenübertragung über das Internet
	- besonders für Umgebungen geeignet, in denen höhere Bandbreite und ein noch höheres Maß an Sicherheit benötigt wird

### Weiterleitung von Netzwerkdatenverkehr

- Standardmaessige Weiterleitung zwischen Subnetzen in verbundenen virtuellen Netzwerken, lokalen Netzwerken und dem Internet

Routingeinstellungen:

- Routingtabelle
	- Mit Routingtabellen werden Regeln für die Weiterleitung von Datenverkehr definiert
	- Erstellung von benutzerdefinierte Routingtabellen, die steuern, wie Pakete zwischen Subnetzen weitergeleitet werden
- Border Gateway Protocol (BGP) 
	- kann für Azure-VPN-Gateways, Azure Route Server oder Azure ExpressRoute verwendet werden, um lokale BGP-Routen an virtuelle Azure-Netzwerke weiterzugeben.

### Filterung von Netzwerkdatenverkehr

Mit virtuellen Azure-Netzwerken können Sie Datenverkehr zwischen Subnetzen wie folgt filtern:

- Netzwerksicherheitsgruppen
	- Azure-Ressourcen, die mehrere Eingangs- und Ausgangssicherheitsregeln enthalten können (Firewall ansatz)
- Virtuelle Netzwerkgeräte
	-  spezielle VMs, die mit einem gehärteten Netzwerkgerät vergleichbar sind.

### Verbindung virtueller Netzwerke

- Virtuelle Netzwerke können mittels Peering miteinander verknüpft werden
- Peering ermöglicht eine direkte Verbindung zwischen zwei virtuellen Netzwerken
- Datenverkehr ist privat durchläuft das Microsoft-Backbone-Netzwerk, aber nie in das öffentliche Internet
- benutzerdefinierten Routen (User-Defined Route, UDR) können die Routingtabellen zwischen Subnetzen innerhalb eines virtuellen Netzwerks oder zwischen virtuellen Netzwerken steuern
- ermöglicht eine bessere Kontrolle über den Netzwerkdatenverkehr


## Konfigurieren eines Netzwerkzugriffs

- Auflisten welche VMs gerade aktiv sind 
```bash
az vm list
```

- IP Adresse der VM in Bash Variable abspeichern
```bash
IPADDRESS="$(az vm list-ip-addresses 
--resource-group "learn-f7f62de7-cae7-41d1-bbb5-dacb3a55a498" 
--name my-vm 
--query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" 
--output tsv)"
```

- Auflisten der aktuellen Network Security Group der VM
```bash
az network nsg list 
--resource-group "learn-f7f62de7-cae7-41d1-bbb5-dacb3a55a498" 
--query '[].name' 
--output tsv
```

- NSG Regeln abrufen
```bash
az network nsg rule list 
--resource-group "learn-f7f62de7-cae7-41d1-bbb5-dacb3a55a498" 
--nsg-name my-vmNSG
```
- Output lesbarer
```bash
az network nsg rule list 
--resource-group "learn-f7f62de7-cae7-41d1-bbb5-dacb3a55a498" 
--nsg-name my-vmNSG 
--query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' 
--output table
```

- Erstellung einer Netzwerk Sicherheits Regel
```bash
az network nsg rule create 
--resource-group "learn-f7f62de7-cae7-41d1-bbb5-dacb3a55a498" 
--nsg-name my-vmNSG 
--name allow-http 
--protocol tcp 
--priority 100 
--destination-port-range 80 
--access Allow
```

## Azure VPN

### VPN-Gateways

- ist eine Art virtuelles Netzwerkgateway
- kann in jedem virtuellen Netzwerk nur ein VPN-Gateway geben

Instanzen von Azure VPN Gateway werden in einem dedizierten Subnetz des virtuellen Netzwerks bereitgestellt und ermöglichen folgende Verbindungen:

- Verbinden von lokalen Rechenzentren mit virtuellen Netzwerken über eine Verbindung von Standort zu Standort (Site-to-Site-Verbindung)
- Verbinden von einzelnen Geräten mit virtuellen Netzwerken über eine Point-to-Site-Verbindung
- Verbinden von virtuellen Netzwerken mit anderen virtuellen Netzwerken über eine Netzwerk-zu-Netzwerk-Verbindung

Beim Einrichten eines VPN-Gateways muss der VPN-Typ angegeben werden (richtlinienbasiert oder routenbasiert):

- Richtlinienbasierte VPN-Gateways
	- geben statisch die IP-Adresse von Paketen an, die über jeden Tunnel verschlüsselt werden sollen
	- wertet jedes Datenpaket mit den IP-Adressen aus, um den Tunnel auszuwählen, über den das Paket gesendet wird
- Routenbasierten VPN-Gateways
	- hier werden IPsec-Tunnel als Netzwerkschnittstelle oder virtuelle Tunnelschnittstelle (Virtual Tunnel Interface) modelliert
	- IP-Routing entscheidet in welche Tunnelschnittstellen gesendet werden sollen
	- stabiler gegenüber Topologieänderungen, wie etwa der Erstellung neuer Subnetze

### Hochverfügbarkeitsszenarien

#### Aktiv/Standby

- zwei Instanzen in einer Aktiv/Standby-Konfiguration
- Bei Unterbrechung der Aktiv Instanz wird verwaltung der Verbindungen automatisch ohne Benutzereingriff an die Standbyinstanz übergeben
- Verbindungen werden während dieses Failovervorgangs kurz unterbrochen
- Ungeplante abbrueche sollten nach 90 sekunden wiede hergestellt sein

#### Aktiv/Aktiv

- Hier wird jeder Instanz eine eindeutige öffentliche IP-Adresse zugewiesen
- erstellt getrennte Tunnel vom lokalen Gerät zu jeder IP-Adresse
- Hochverfügbarkeit erweitern, indem ein zusätzliches VPN-Gerät lokal bereitgestellt wird

#### ExpressRoute-Failover

- VPN-Gateway als sicheren Failoverpfad für ExpressRoute-Verbindungen
- ExpressRoute-Verbindungen sind von Haus aus resilient
- nicht immun gegen physische Probleme bei den Kabeln, oder gegen Ausfälle, die den gesamten ExpressRoute-Standort betreffen

#### Zonenredundante Gateways

- VPN- und ExpressRoute-Gateways können in Regionen, die Verfügbarkeitszonen unterstützen, in einer zonenredundanten Konfiguration bereitgestellt werden
- bringt Resilienz, Skalierbarkeit und eine höhere Verfügbarkeit für die Gateways des virtuellen Netzwerks mit sich
- Bereitstellung von Gateways in Azure-Verfügbarkeitszonen werden die Gateways innerhalb einer Region physisch und logisch getrennt
- Gleichzeitig wird Konnektivität des lokalen Netzwerks mit Azure vor Ausfällen auf Zonenebene geschützt
- sind verschiedene Gateway-SKUs (Stock Keeping Units) erforderlich, und es werden öffentliche Standard-IP-Adressen anstelle von öffentlichen Basic-IP-Adressen verwendet

### Azure ExpressRoute

- kann lokale Netzwerke über eine private Verbindung auf die Cloud von Microsoft ausdehnen
- Verbindung wird als ExpressRoute-Leitung bezeichnet
- es können Verbindungen mit Microsoft-Clouddiensten hergestellt werden, z. B. Microsoft Azure und Microsoft 365
- können Büros, Rechenzentren oder andere Einrichtungen mit der Microsoft-Cloud verbinden, jeder Standort mit eigener ExpressRoute-Leitung
- Konnektivität kann über ein Any-to-Any-Netzwerk (IP VPN), ein Point-to-Point-Ethernet-Netzwerk oder eine virtuelle Querverbindung über einen Konnektivitätsanbieter in einer Co-Location-Einrichtung bereitgestellt werden
- nutzen nicht das öffentliche Internet
- Bieten gleichmäßige Latenz, hoehere Sicherheit, groessere Zuverlaessigkeit und hoehere Geschwindigkeit als Internetverbindungen

#### Vorteile von ExpressRoute

- Verbindung mit Microsoft-Clouddiensten in allen Regionen einer geopolitischen Region
- Globale Konnektivität mit Microsoft-Diensten in allen Regionen mit ExpressRoute Global Reach
- Dynamisches Routing zwischen lokalem Netzwerk und Microsoft über das Border Gateway Protocol (BGP)
- Integrierte Redundanz an jedem Peeringort, um eine höhere Zuverlässigkeit zu erzielen

#### Globale Konnektivitaet 

- ExpressRoute Global Reach zum Austausch von Daten zwischen lokalen Standorten, indem Sie Ihre ExpressRoute-Leitungen verbinden
- z.B. Europaeisches Rechenzentrum und Asiatisches Buero sind beide über ExpressRoute-Leitungen mit dem Microsoft-Netzwerk verbunden sodass Daten uebertragen werden koennen ohne public Internet

#### Dynamisches Routing

- Mit Border Gateway Protocol (BGP) werden Routen zwischen lokalen Netzwerken und in Azure ausgeführten Ressourcen ausgetauscht
- ermöglicht ein dynamisches Routing zwischen lokalem Netzwerk und Diensten, die in Microsoft Cloud ausgeführt werden

#### Integrierte Redundanz

- Konnektivitätsanbieter verwenden redundante Geräte
- Ergänzung dieser Funktion können Sie mehrere Leitungen konfigurieren

#### ExpressRoute-Konnektivitaetsmodelle

- CloudExchange-Housing
	- bezieht sich auf Private Ressourcen die sich physisch an einem CloudExchange befinden z.B. bei einem ISP
	- können eine virtuelle Querverbindung mit der Microsoft-Cloud anfordern
- Point-to-Point-Ethernet-Verbindung
	- Point-to-Point-Ethernetverbindung bezieht sich auf die Verwendung einer Point-to-Point-Verbindung der Einrichtung mit der Microsoft-Cloud
- Any-to-Any-Netzwerke
	- Integration von privaten WAN in Azure
	- Azure wird in Ihre WAN-Verbindung integriert, um eine Verbindung wie zwischen Ihrem Rechenzentrum und beliebigen Niederlassungen zu bieten
- Direkt von ExpressRoute-Standorten
	- direktverbindung mit globalem Microsoft Netzwerk
	- strategische verbindung über die ganze Welt verteilten Peeringstandorten
	- bietet duale Konnektivität mit 100 oder 10 GBit/s, die eine Aktiv/Aktiv-Konnektivität nach Maß unterstützt

## Azure DNS

Ist ein Hostingdienst für DNS-Domänen, der eine Namensauflösung mittels Microsoft Azure-Infrastruktur bietet

### Vorteile von Azure DNS

- Zuverlaessigkeit und Leistung
	- Domains werden im globalen Azure-Netzwerk von Domänennamenservern gehostet und bieten Resilienz und Hochverfügbarkeit
	- Anycast-Netzwerke werden verwendet, sodass jede DNS-Abfrage vom am nächsten liegenden verfügbaren DNS-Server beantwortet wird
- Sicherheit
	- Rollenbasierte Zugriffssteuerung in Azure (Azure RBAC), um zu steuern, wer Zugriff auf bestimmte Aktionen hat
	- Aktivitätsprotokolle, um nachzuverfolgen, wie ein Benutzer Ressourcen geändert hat, oder um im Rahmen der Problembehandlung Fehler zu finden
	- Ressourcensperre, um ein Abonnement, eine Ressourcengruppe oder eine Ressource zu sperren
	- Sperre verhindert, dass andere Benutzer versehentlich wichtige Ressourcen löschen oder ändern
- Benutzerfreundlichkeit
- Benutzerdefinierbare virtuelle Netzwerke
	- unterstützt auch private DNS-Domänen
	- koennen in privaten virtuellen Netzwerken anstelle der von Azure bereitgestellten Namen Ihre eigenen benutzerdefinierten Domänennamen verwenden
- Aliaseinträge
	- unterstützt Aliasdatensatzgruppen
	- verwenden, um auf eine Azure-Ressource zu verweisen, beispielsweise eine öffentliche Azure-IP-Adresse, ein Azure Traffic Manager-Profil oder einen Azure CDN-Endpunkt (Azure Content Delivery Network)
	- Bei IP aenderung der Ressource wird der Alias automatisch angepasst

