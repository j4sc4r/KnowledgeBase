# Azure Compute- und Azure-Netzwerkdienste

## Azure-VMs

VMs stellen IaaS (Infrastructure-as-a-Service) in Form eines virtualisierten Servers zur Verfügung.

VMs sind ideal bei folgenden Szenarien:
- Vollständige Kontrolle über das Betriebssystem
- Die Möglichkeit, benutzerdefinierte Software auszuführen
- Die Möglichkeit, benutzerdefinierte Hostingkonfigurationen zu verwenden

Bereits erstellte Images koennen benutzt werden um spezifische Software noch schneller auf einer VM bereitzustellen.

### Skalieren der Azure-VMs

- einzelne VMs koennen für Test-, Entwicklungs- oder kleinere Aufgaben benutzt werden
- VMs koennen gruppiert werden, um Hochverfügbarkeit, Skalierbarkeit und Redundanz zu gewährleisten
- Azure kann Gruppierung von VMs mit Features wie Skalierungsgruppen und Verfügbarkeitssätzen verwalten

#### VM-Skalierungsgruppen

- in Azure koennen identische VMs mit Load Balancing erstellt und verwaltet werden
- Skalierungsgruppen können eine große Anzahl von VMs innerhalb weniger Minuten zentral verwalten, konfigurieren und aktualisieren
- VM-Instanzen koennen als Reaktion auf die Nachfrage oder einen definierten Zeitplan automatisch erhöht oder verringert werden
- stellen auch automatisch Load Balancing bereit

#### VM-Verfuegbarkeitsgruppen

- sind so konzipiert, dass Updates der VMs verschoben werden und dass Stromversorgung und Netzwerkverbindungen unabhängig sind, um zu verhindern, dass Sie beim einem Ausfall eines einzelnen Netzwerks oder bei einem Stromausfall alle Ihre VMs verlieren

Erreicht wird das auf zwei Arten:
- Updatedomain
	- werden VMs gruppiert, die gleichzeitig neu gestartet werden können
	- Gleichzeitiges Updaten und sicher sein, dass nur eine Gruppe in einer Updatedomäne gleichzeitig offline ist
	- Wenn Updategruppe den Updateprozess durchläuft, werden 30 Minuten Zeit für die Wiederherstellung gewährt, bevor die Wartung in der nächsten Updatedomäne gestartet wird
- Fehlerdomain
	- werden VMs mit einer gemeinsamen Stromquelle und einem gemeinsamen Netzwerkswitch gruppiert
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

Um eine extension der VM hinzuzufuegen:

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

- verwendet die benutzerdefinierte Skripterweiterung, um ein Bash-Skript auf Ihrer VM auszuführen

### Azure Virtual Desktop

- ist ein in der Cloud ausgeführter Dienst für die Desktop- und Anwendungsvirtualisierung
- funktioniert ueber Geraete und Betriebssysteme hinweg, mit Apps die auf Remote Desktops zugreifen koennen und den meisten Browsern
- bietet zentralisierte Sicherheitsverwaltung für die Desktops von Benutzer*innen mit Microsoft Entra ID
- mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) zum Sichern von Benutzeranmeldungen koennen aktiviert werden
- Datensicherheitserhoehung durch differenzierte und rollenbasierte Zugriffssteuerung der Benutzer
- hier werden die Daten und Apps von der lokalen Hardware getrennt

## Azure-Container

Container sind eine gute Wahl, wenn Sie mehrere Instanzen einer Anwendung auf einem einzelnen Hostcomputer ausführen möchten

### Was sind Container


![[Azure_VMs.png]] ![[Azure_Containers.png]]
- sind eine Virtualisierungsumgebung
- können mehrere Container auf einem einzigen physischen oder virtuellen Host ausführen
- Das Container Betriebssystem wird nicht verwaltet
- sind schlank und so konzipiert, dass sie dynamisch erstellt, skaliert und beendet werden können
- stellen eine weniger aufwendige, agilere Methode dar als mehrere VMs zu installieren
- sind so konzipiert, dass Sie bei Bedarf auf Änderungen reagieren können
- im Fall eines Absturzes oder einer Hardwareunterbrechung koennen sie schnell neu gestartet werden


### Azure Container Instances

- bietet die schnellste und einfachste Möglichkeit, einen Container in Azure auszuführen, ohne VMs verwalten oder zusätzliche Dienste einsetzen zu müssen
- ist ein PaaS-Angebot (Platform as a Service)
- Container hochladen und dann durch den Dienst ausführen lassen

### Azure Container Apps

- ähnelt in vielerlei Hinsicht einer Containerinstanz
- können Sie sofort loslegen und müssen keine Container verwalten
- hat zusätzliche Vorteile, z. B. die Möglichkeit, Lastenausgleich und Skalierung zu integrieren

### Azure Kubernetes Service

- ist ein Containerorchestrierungsdienst
- Orchestrierungsdienst verwaltet den Lebenszyklus von Containern
- Wenn eine Containerflotte bereitgestellt wird, kann AKS die Flottenverwaltung einfacher und effizienter gestalten.

## Azure Functions

- ist eine ereignisgesteuerte, serverlose Computeoption, die keine Wartung von VMs oder Containern erfordert
- Bei Azure Functions wird die Funktion durch ein Ereignis ausgelöst, sodass Sie keine Ressourcen bereitstellen müssen, wenn keine Ereignisse vorhanden sind

Vorteile von Azure Functions:
- eignet sich, wenn sich nur um den Code zum Ausführen Ihres Diensts und nicht die zugrunde liegende Plattform oder Infrastruktur gekuemmert werden muss
- wird häufig verwendet, wenn Sie als Reaktion auf ein Ereignis (häufig über eine REST-Anforderung), einen Timer oder eine Nachricht von einem anderen Azure-Dienst eine Aufgabe ausführen müssen und wenn diese Aufgabe schnell (innerhalb von Sekunden oder schneller) erledigt werden kann
- wird automatisch nach Bedarf skaliert und ist somit eine gute Wahl, wenn der Bedarf variabel ist
- führt Ihren Code aus, wenn er ausgelöst wird, und hebt die Zuteilung von Ressourcen automatisch auf, wenn die jeweilige Funktion beendet wurde
- Hier wird die CPU-Zeit berechnet als Zahlungsanforderung

## Azure App Service

- ermöglicht Ihnen das Erstellen und Hosten von Web-Apps, Hintergrundaufträgen, mobilen Back-Ends und RESTful-APIs
- bietet automatische Skalierung und hohe Verfügbarkeit
- unterstuetzt Windows und Linux
- ermöglicht automatisierte Bereitstellungen über GitHub, Azure DevOps oder ein beliebiges Git-Repository zur Unterstützung eines Continuous Deployment-Modells

### Typen von App-Diensten

Mit App Service können Sie die meisten App-Dienstformate hosten, einschließlich der folgenden:
- Web-Apps
- API-Apps
- WebJobs
- Mobile Apps

App Service übernimmt die meisten Infrastrukturentscheidungen, die Sie beim Hosting von Apps im Internet treffen:
- Funktionen zur Bereitstellung und Verwaltung sind in die Plattform integriert
- Endpunkte koennen gesichert werden
- Websites lassen sich schnell skalieren, um hohe Datenverkehrslasten zu bewaeltigen
- Die integrieten Load Balancing und Traffic Manager Funktionen ermoeglichen Hochverfuegbarkeit

## Azure-Netzwerke

Mit virtuellen Azure-Netzwerken und virtuellen Subnetzen können Azure-Ressourcen wie etwa VMs, Web-Apps und Datenbanken untereinander, mit Benutzer*innen im Internet sowie mit Ihren lokalen Clientcomputern kommunizieren. 

Funktionen: 
- Isolation und Segmentierung 
- Internetkommunikation
- Kommunikation zwischen Azure-Ressourcen
- Kommunikation mit lokalen Ressourcen
- Weiterleitung von Netzwerkdatenverkehr 
- Verbindung virtueller Netzwerke

Virtuelle Azure-Netzwerke unterstützen sowohl öffentliche als auch private Endpunkte, um die Kommunikation zwischen externen oder internen Ressourcen mit anderen internen Ressourcen zu ermöglichen.

- Öffentliche Endpunkte haben eine öffentliche IP-Adresse, auf die von jedem Ort der Welt aus zugegriffen werden kann.
- Private Endpunkte sind in einem virtuellen Netzwerk enthalten und weisen eine private IP-Adresse im Adressraum des virtuellen Netzwerks auf.

### Isolation und Segmentierung

- Azure Virtual Network ermöglicht die Erstellung mehrerer isolierter virtueller Netzwerke
- Bei Einrichtung definieren Sie einen privaten IP-Adressraum, indem Sie entweder öffentliche oder private IP-Adressbereiche verwenden
- IP-Adressbereich ist nur innerhalb des virtuellen Netzwerks vorhanden und kann nicht über das Internet geroutet werden
- IP Bereich kann in Subnetze unterteilt werden
- Integrierter Dienst zur Namensaufloesung
- kann aber auch mit externen DNS konfiguriert werden

### Internetkommunikation

Sie können eingehende Internetverbindungen zulassen, indem Sie einer Azure-Ressource eine öffentliche IP-Adresse zuweisen oder die VM hinter einem öffentlichen Lastenausgleich platzieren.

### Kommunikation zwischen Azure-Ressourcen

Es empfiehlt sich, eine sichere Kommunikation zwischen Azure-Ressourcen zu ermöglichen. Dazu haben Sie zwei Möglichkeiten:

- Virtuelle Netzwerke können nicht nur eine Verbindung mit VMs herstellen, sondern auch mit anderen Azure-Ressourcen. Hierzu zählen beispielsweise die App Service-Umgebung für Power Apps, Azure Kubernetes Service und Azure-VM-Skalierungsgruppen.
- Mithilfe von Dienstendpunkten können Sie eine Verbindung mit anderen Azure-Ressourcentypen herstellen
- Bei diesem Ansatz können Sie mehrere Azure-Ressourcen mit virtuellen Netzwerken verknüpfen, um die Sicherheit zu erhöhen und ein optimales Routing zwischen Ressourcen sicherzustellen.

### Kommunikation mit lokalen Ressourcen

- moeglichkeit lokale Ressourcen mit dem Azure Abonnement zu verknuepfen
- Es kann ein Netzwerk erstellt werden was die Cloud und die Lokale Umgebung abdeckt

3 Mechanismen fuer die herstellungen dieser Konnektivitaet: 

- Point-to-Site-VPN 
	- VPN besteht zwischen einem Computer außerhalb Ihrer Organisation zurück in das Unternehmensnetzwerk
	- Clientcomputer initiiert eine verschluesselte VPN-Verbindung
- Site-to-Site-VPN
	- verbinden Ihr lokales VPN-Gerät oder -Gateway mit dem Azure-VPN-Gateway in einem virtuellen Netzwerk
	- Verbindung ist verschlüsselt und internetbasiert
- Azure ExpressRoute
	- bietet dedizierte private Konnektivität mit Azure ohne eine Datenübertragung über das Internet
	- besonders für Umgebungen geeignet, in denen Sie eine höhere Bandbreite und ein noch höheres Maß an Sicherheit benötigen

### Weiterleitung von Netzwerkdatenverkehr

Azure leitet standardmäßig Datenverkehr zwischen Subnetzen in beliebigen verbundenen virtuellen Netzwerken, lokalen Netzwerken und dem Internet weiter.

Routingeinstellungen:

- Mit Routingtabellen können Sie Regeln für die Weiterleitung von Datenverkehr definieren. Sie können benutzerdefinierte Routingtabellen erstellen, die steuern, wie Pakete zwischen Subnetzen weitergeleitet werden.
- Ein Border Gateway Protocol (BGP) kann für Azure-VPN-Gateways, Azure Route Server oder Azure ExpressRoute verwendet werden, um lokale BGP-Routen an virtuelle Azure-Netzwerke weiterzugeben.

### Filterung von Netzwerkdatenverkehr

Mit virtuellen Azure-Netzwerken können Sie Datenverkehr zwischen Subnetzen wie folgt filtern:

- Netzwerksicherheitsgruppen sind Azure-Ressourcen, die mehrere Eingangs- und Ausgangssicherheitsregeln enthalten können (Firewall ansatz)
- Virtuelle Netzwerkgeräte sind spezielle VMs, die mit einem gehärteten Netzwerkgerät vergleichbar sind.

### Verbindung virtueller Netzwerke

- Virtuelle Netzwerke können mittels Peering miteinander verknüpft werden
- Peering ermöglicht eine direkte Verbindung zwischen zwei virtuellen Netzwerken
- Datenverkehr ist privat durchläuft das Microsoft-Backbone-Netzwerk, aber nie in das öffentliche Internet
- ermöglicht es Ressourcen in den einzelnen virtuellen Netzwerken, miteinander zu kommunizieren

Mit benutzerdefinierten Routen (User-Defined Route, UDR) können Sie die Routingtabellen zwischen Subnetzen innerhalb eines virtuellen Netzwerks oder zwischen virtuellen Netzwerken steuern. Dies ermöglicht eine bessere Kontrolle über den Netzwerkdatenverkehr.


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

Ein virtuelles privates Netzwerk (VPN) verwendet einen verschlüsselten Tunnel in einem anderen Netzwerk. VPNs werden in der Regel bereitgestellt, um zwei oder mehr vertrauenswürdige private Netzwerke über ein nicht vertrauenswürdiges Netzwerk (in der Regel das öffentliche Internet) miteinander zu verbinden.

### VPN-Gateways

- ist eine Art virtuelles Netzwerkgateway
- kann in jedem virtuellen Netzwerk nur ein VPN-Gateway geben

Instanzen von Azure VPN Gateway werden in einem dedizierten Subnetz des virtuellen Netzwerks bereitgestellt und ermöglichen folgende Verbindungen:

- Verbinden von lokalen Rechenzentren mit virtuellen Netzwerken über eine Verbindung von Standort zu Standort (Site-to-Site-Verbindung)
- Verbinden von einzelnen Geräten mit virtuellen Netzwerken über eine Point-to-Site-Verbindung
- Verbinden von virtuellen Netzwerken mit anderen virtuellen Netzwerken über eine Netzwerk-zu-Netzwerk-Verbindung

Beim Einrichten eines VPN-Gateways müssen Sie den VPN-Typ angeben (richtlinienbasiert oder routenbasiert

- Richtlinienbasierte VPN-Gateways
	- geben statisch die IP-Adresse von Paketen an, die über jeden Tunnel verschlüsselt werden sollen. Dieser Gerätetyp wertet jedes Datenpaket mit den IP-Adressen aus, um den Tunnel auszuwählen, über den das Paket gesendet wird.
- Routenbasierten VPN-Gateways
	- werden IPsec-Tunnel als Netzwerkschnittstelle oder virtuelle Tunnelschnittstelle (Virtual Tunnel Interface) modelliert
	- IP-Routing entscheidet in welche Tunnelschnittstellen gesendet werden sollen
	- stabiler gegenüber Topologieänderungen, wie etwa der Erstellung neuer Subnetze

### Hochverfügbarkeitsszenarien

#### Aktiv/Standby

- zwei Instanzen in einer Aktiv/Standby-Konfiguration
- Bei  Unterbrechung der Aktiv Instanz wird verwaltung der Verbindungen automatisch ohne Benutzereingriff an die Standbyinstanz übergeben
- Verbindungen werden während dieses Failovervorgangs unterbrochen
- Geplant innerhalb weniger sekunden wieder erreichbar
- Ungeplant innerhalb von 90 Sekunden

#### Aktiv/Aktiv

- Hier weisen Sie jeder Instanz eine eindeutige öffentliche IP-Adresse zu
- erstellen Sie getrennte Tunnel vom lokalen Gerät zu jeder IP-Adresse
- hohe Verfügbarkeit erweitern, indem Sie ein zusätzliches VPN-Gerät lokal bereitstellen

#### ExpressRoute-Failover

- VPN-Gateway als sicheren Failoverpfad für ExpressRoute-Verbindungen zu konfigurieren
- ExpressRoute-Verbindungen sind von Haus aus resilient
- nicht immun gegen physische Probleme bei den Kabeln, über die Verbindungen hergestellt werden, oder gegen Ausfälle, die den gesamten ExpressRoute-Standort betreffen
- Risiko eines Ausfalls einer ExpressRoute-Verbindung besteht, können Sie auch ein VPN-Gateway bereitstellen, das das Internet als alternative Verbindungsmethode verwendet

#### Zonenredundante Gateways

- VPN- und ExpressRoute-Gateways können in Regionen, die Verfügbarkeitszonen unterstützen, in einer zonenredundanten Konfiguration bereitgestellt werden
- bringt Resilienz, Skalierbarkeit und eine höhere Verfügbarkeit für die Gateways des virtuellen Netzwerks mit sich
- Bereitstellung von Gateways in Azure-Verfügbarkeitszonen werden die Gateways innerhalb einer Region physisch und logisch getrennt
- Gleichzeitig wird Konnektivität Ihres lokalen Netzwerks mit Azure vor Ausfällen auf Zonenebene geschützt
- sind verschiedene Gateway-SKUs (Stock Keeping Units) erforderlich, und es werden öffentliche Standard-IP-Adressen anstelle von öffentlichen Basic-IP-Adressen verwendet

### Azure ExpressRoute

- können Sie Ihre lokalen Netzwerke über eine private Verbindung auf die Cloud von Microsoft ausdehnen
- Verbindung wird als ExpressRoute-Leitung
- können Sie Verbindungen mit Microsoft-Clouddiensten herstellen, z. B. Microsoft Azure und Microsoft 365
- können Sie Büros, Rechenzentren oder andere Einrichtungen mit der Microsoft-Cloud verbinden. Jeder Standort hätte dabei eine eigene ExpressRoute-Leitung
- Konnektivität kann über ein Any-to-Any-Netzwerk (IP VPN), ein Point-to-Point-Ethernet-Netzwerk oder eine virtuelle Querverbindung über einen Konnektivitätsanbieter in einer Co-Location-Einrichtung bereitgestellt werden
- nutzen nicht das öffentliche Internet
- koennen gleichmäßige Latenz sowie höhere Sicherheit, größere Zuverlässigkeit und schnellere Geschwindigkeit als herkömmliche Verbindungen über das Internet bieten

#### Vorteile von ExpressRoute

- Verbindung mit Microsoft-Clouddiensten in allen Regionen einer geopolitischen Region
- Globale Konnektivität mit Microsoft-Diensten in allen Regionen mit ExpressRoute Global Reach
- Dynamisches Routing zwischen Ihrem Netzwerk und Microsoft über das Border Gateway Protocol (BGP)
- Integrierte Redundanz an jedem Peeringort, um eine höhere Zuverlässigkeit zu erzielen

#### Globale Konnektivitaet 

- ExpressRoute Global Reach zum Austausch von Daten zwischen Ihren lokalen Standorten aktivieren, indem Sie Ihre ExpressRoute-Leitungen verbinden
- z.B. Europaeisches Rechenzentrum und Asiatisches Buero sind beide über ExpressRoute-Leitungen mit dem Microsoft-Netzwerk verbunden sodass Daten uebertragen werden koennen ohne public Internet

#### Dynamisches Routing

- Mit Border Gateway Protocol (BGP) werden Routen zwischen lokalen Netzwerken und in Azure ausgeführten Ressourcen ausgetauscht
- ermöglicht ein dynamisches Routing zwischen Ihrem lokalen Netzwerk und Diensten, die in Microsoft Cloud ausgeführt werden

#### Integrierte Redundanz

- Konnektivitätsanbieter verwenden redundante Geräte
- Ergänzung dieser Funktion können Sie mehrere Leitungen konfigurieren

#### ExpressRoute-Konnektivitaetsmodelle

- CloudExchange-Housing
	- bezieht sich auf Private Ressourcen die sich physisch an einem CloudExchange befinden z.B. bei einem ISP
	- Wenn verbunden können Sie eine virtuelle Querverbindung mit der Microsoft-Cloud anfordern
- Point-to-Point-Ethernet-Verbindung
	- Point-to-Point-Ethernetverbindung bezieht sich auf die Verwendung einer Point-to-Point-Verbindung Ihrer Einrichtung mit der Microsoft-Cloud
- Any-to-Any-Netzwerke
	- Integration von privaten WAN in Azure
	- Azure wird in Ihre WAN-Verbindung integriert, um eine Verbindung wie zwischen Ihrem Rechenzentrum und beliebigen Niederlassungen zu bieten
- Direkt von ExpressRoute-Standorten
	- direktverbindung mit globalem Microsoft Netzwerk
	- strategische verbindung über die ganze Welt verteilten Peeringstandorten
	- bietet duale Konnektivität mit 100 oder 10 GBit/s, die eine Aktiv/Aktiv-Konnektivität nach Maß unterstützt

## Azure DNS

- ist ein Hostingdienst für DNS-Domänen, der eine Namensauflösung mittels Microsoft Azure-Infrastruktur bietet

### Vorteile ovn Azure DNS

- Zuverlässigkeit und Leistung
	- Domains werden im globalen Azure-Netzwerk von Domänennamenservern gehostet und bieten Resilienz und Hochverfügbarkeit
	- Anycast-Netzwerke verwendet, sodass jede DNS-Abfrage jeweils vom am nächsten liegenden verfügbaren DNS-Server beantwortet wird
- Sicherheit
	- Rollenbasierte Zugriffssteuerung in Azure (Azure RBAC), um zu steuern, wer Zugriff auf bestimmte Aktionen für Ihre Organisation hat
	- Aktivitätsprotokolle, um nachzuverfolgen, wie ein Benutzer in Ihrer Organisation eine Ressource geändert hat, oder um im Rahmen der Problembehandlung Fehler zu finden
	- Ressourcensperre, um ein Abonnement, eine Ressourcengruppe oder eine Ressource zu sperren. Eine Sperre verhindert, dass andere Benutzer in Ihrer Organisation versehentlich wichtige Ressourcen löschen oder ändern
- Benutzerfreundlichkeit
- Benutzerdefinierbare virtuelle Netzwerke
	- unterstützt auch private DNS-Domänen
	- in privaten virtuellen Netzwerken anstelle der von Azure bereitgestellten Namen Ihre eigenen benutzerdefinierten Domänennamen verwenden
- Aliaseinträge
	- unterstützt Aliasdatensatzgruppen
	- können einen Aliaseintragssatz verwenden, um auf eine Azure-Ressource zu verweisen, beispielsweise eine öffentliche Azure-IP-Adresse, ein Azure Traffic Manager-Profil oder einen Azure CDN-Endpunkt (Azure Content Delivery Network)
	- Bei IP aenderung der Ressource wird der Alias automatisch angepasst

