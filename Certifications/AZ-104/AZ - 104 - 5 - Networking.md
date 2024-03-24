# AZ - 104 - 5 - Networking

# Virtual Network (VNets)

Eine virtuelle Darstellung des On-Premise Netzwerks in der Cloud.

- Kann mit andern VNets verlinkt werden wenn der CIDR nicht ueberlappt
	- On-Premise und Cloud

## Subnetze

Ein VNet kann in Subnetze unterteilt werden. Dies ist eine logische Aufgliederung des Virtuellen Netzwerks. 

>[!note]
>Azure reserviert die ersten 4 (0-3) und die letzte (255) IP-Adresse in jedem Subnetz

# Netzwerksicherheitsgruppen (NSG)

Enthält eine Liste mit Sicherheitsregeln, die eingehenden oder ausgehenden Netzwerkdatenverkehr zulassen oder verweigern.

- Kann einem Subnetz oder einer Netzwerkschnittstelle zugeordnet werden
- Kann mehrfach zugeordnet werden
- Standardregeln sind `DenyAllInbound` Datenverkehr und `AllowInternetOutbound` Datenverkehr

## Anwendungssicherheitsgruppen

Mit Anwendungssicherheitsgruppen können Sie die Netzwerksicherheit als natürliche Erweiterung einer Anwendungsstruktur konfigurieren und virtuelle Computer gruppieren sowie auf der Grundlage dieser Gruppen Netzwerksicherheitsrichtlinien definieren.

# Azure DNS 

Verwaltet und löst Domänennamen in einem virtuellen Netzwerk auf.
Jede Domäne hat eine DNS-Zone, und jeder DNS-Eintrag für Ihre Domäne wird in der DNS-Zone erstellt.

Beispielsweise kann contoso.com eine Reihe von DNS-Einträgen enthalten, wie mail.contoso.com

>[!note]
>Sie müssen nicht Eigentümer eines Domainnamens sein, um eine DNS-Zone mit diesem Domainnamen zu erstellen. Sie müssen jedoch Eigentümer der Domäne sein, um die Domäne zu konfigurieren.

## Resourceneintragssaetze

>[!important]
>Es gibt einen Unterschied zwischen DNS-Datensätzen und einzelnen DNS-Datensätzen.

Ein Resourceneintragssaetze ist eine Sammlung von Resourceneintraegen in einer Zone, die denselben Namen und denselben Typ haben.

## Private DNS Zonen

Private Zonen bieten Namensauflösung für VMs innerhalb eines virtuellen Netzwerks und über VNets hinweg, ohne dass eine benutzerdefinierte DNS-Lösung erstellt werden muss.

Die Namensauflösung über mehrere virtuelle Netzwerke hinweg ist wahrscheinlich die häufigste Verwendung für private DNS-Zonen.

Sie ermöglichen die Verwendung benutzerdefinierter Domänennamen innerhalb eines VNet.

## Alias

A-Records und CNAME-Records unterstützen keine direkte Verbindung zu Azure-Ressourcen wie Load Balancern. Die Lösung sind Alias-Einträge.

Aktivieren Sie eine Zonen-Apex-Domäne, um andere Azure-Ressourcen aus der DNS-Zone zu referenzieren.

Der Hauptvorteil ist, dass Sie DNS-Einträge einer Azure-Ressource wie einer öffentlichen IP zuweisen können. Wenn sich die öffentliche IP ändert, wird auch der DNS-Eintrag automatisch aktualisiert.

# VNet Peering

- regionales vnet peering 
	- verbindet Vnets in derselben Region  
- globales vnet-Peering  
	- Verbindet Netze in verschiedenen Regionen  
	- alle Public-Cloud-Regionen, aber keine Government-Cloud-Regionen  
- der Verkehr zwischen den gepeerten Netzen ist privat  
- hohe Leistung  
- keine Ausfallzeiten bei der Einrichtung des Peerings

## Dienstverkettung

wenn VNET 1 und 2 gepeert werden und 2 und 3, 1 und 3 nicht gepaart werden. Mit anderen Worten: Peering ist nicht transitiv.  

Benutzerdefinierte Routen und Dienstverkettungen können konfiguriert werden, um die Transitivität zu gewährleisten.

# Routen und Endpunkte im Netzwerk

- System-Routen 
	- bezieht sich auf das Standard-Routing, das von Azure automatisch durchgeführt wird  
	- im Gegensatz zu Benutzer-Routen    
	- leitet den Netzwerkverkehr zwischen  
		- VMs  
			- im gleichen Subnetz  
			- verschiedene Subnetze im gleichen VNet  
			- Datenfluss von VM zum Internet  
		- On-Prem-Netze  
		- Internet  
- Routing-Tabellen  
	- enthalten Informationen über Systemrouten  
	- Satz von Regeln, die angeben, wie Pakete weitergeleitet werden sollen  
	- den Subnetzen zugeordnet  
	- übereinstimmende Ziele, die sind:  
		- IP-Adresse  
		- VNet-Gateway  
		- Virtuelles Gerät  
		- Internet  
	- Wenn keine passende Route gefunden werden kann, wird das Paket verworfen.

- Benutzerdefinierte Routen  
	- im Gegensatz zu Systemrouten  
	- benutzerdefinierte Konfiguration, zum Beispiel:  
		- Leiten des Datenverkehrs an eine VM, die Routing oder Firewalling durchführt

>[!note]
>Jede Routentabelle kann mit mehreren Subnetzen verbunden sein, aber ein Subnetz kann nur mit einer einzigen Routentabelle verbunden sein.

## Endpunkte

Verwendet für Dienste wie Azure AD, Cosmos DB, Storage

>Ein virtueller Netzwerkdienst-Endpunkt liefert die Identität Ihres virtuellen Netzwerks an den Azure-Dienst.

Normalerweise verwendet der Verkehr von einem Azure VNet eine öffentliche IP-Adresse als Quelladresse.  

Service-Endpunkte schalten diesen Datenverkehr so um, dass eine private Adresse des virtuellen Netzwerks als Quell-IP-Adresse verwendet wird, wenn auf den Azure-Dienst von einem virtuellen Netzwerk aus zugegriffen wird.  

Durch diese Umstellung können Sie auf die Dienste zugreifen, ohne dass reservierte, öffentliche IP-Adressen in IP-Firewalls verwendet werden müssen.

- Und warum?  
	- Verbesserte Sicherheit für Azure-Service-Ressourcen  
		- Private VNet-Adressräume können sich überschneiden und sind daher nicht geeignet, den Ursprung des Datenverkehrs zu identifizieren.  
			- daher werden normalerweise öffentliche IP-Adressen verwendet  
		- vollständiger Ausschluss des öffentlichen Internetzugangs zu Ressourcen  
			- Zulassung von Datenverkehr nur aus Ihrem virtuellen Netzwerk  
	- Optimales Routing vom VNet  
	- hält den Datenverkehr im Azure Backbone-Netzwerk  
	- keine Notwendigkeit für reservierte öffentliche IP-Adressen in VNets  
	- keine NAT- oder Gateway-Geräte erforderlich, um Service-Endpunkte einzurichten

## Azure Private Link

- Vereinfacht die Netzwerkarchitektur  
- eliminiert die Datenexposition im öffentlichen Internet  
	- Der Datenverkehr bleibt im Microsoft-Netzwerk  
- global, keine Einschränkungen  
- Zugriff über  
	- privates Peering  
	- VPN-Tunnel vom lokalen oder gepeerten VNet

# Azure Load Balancer 

Verteilt den eingehenden Verkehr auf Backend-Ressourcen.  

Zwei Arten: öffentlich und intern  

- öffentlich  
	- ordnet die öffentliche IP und den Port des eingehenden Datenverkehrs der privaten IP und dem Port der VM zu  
	- Zuordnung des Antwortverkehrs von der VM  
	- Lastausgleichsregeln zur Verteilung auf mehrere VMs oder Dienste  
- intern  
	- leitet den Verkehr zu Ressourcen innerhalb eines VNetzes oder die ein VPN für den Zugriff auf Azure verwenden  
	- Frontend-IP-Adressen und VNets sind nie direkt dem Internet-Endpunkt ausgesetzt  
	- Beispiel interner Load Balancer:  
		- Empfangen von Datenbankanfragen und Verteilen an Backend-SQL-Server  
	- Vor-Ort-übergreifendes VNet  
		- Lastausgleich von On-Premise zu VMs im gleichen VNet  
- Sitzungsaufrechterhaltung  
	- wie der Verkehr vom Client behandelt werden soll  
	- Beispiel: Einkaufswagen  
	- Standard: keine  
		- wird von jeder VM behandelt  
	- Client-IP  
		- aufeinanderfolgende Anfragen von der gleichen Client-IP werden von der gleichen VM behandelt  
	- Client-IP und Protokoll  
		- gleich kombiniert mit Protokoll  
- Health Probes (Integritaetstest)  
	- Ermöglicht Load Balancer die Überwachung des Anwendungsstatus  
	- Entfernt oder fügt VMS aus der Load Balancer Rotation hinzu, basierend auf der Antwort auf die Gesundheitstests 
	- Wenn die Prüfung fehlschlägt, sendet der Lastverteiler keine neuen Verbindungen mehr an ihn.

# Azure Application Gateway

Verwaltet Anfragen, die Clientanwendungen an eine Web-App senden.

- Verwendet Routing auf Anwendungsebene 
	- Routen zum Pool von Webservern 
	- basierend auf der URL einer Anfrage 
	- kann sein 
		- VMs 
		- VM Skalierungsgruppen (Scale Sets) 
		- Azure App-Dienst

# IP Adressen Schema

3 Ranges fuer nicht routbare IP adressen im internen Netzwerk:

- 10.0.0.0 - 10.255.255.255
- 172.16.0.0 - 172.32.255.255
- 192.168.0.0 - 192.168.255.255
- VNets sind anders als on premise Netzwerke
	- koennen hoch- und runterskaliert werden
	- bereitstellung erfolgt in sekunden
	- kein physisches Geraet wird benutzt
	- Virtuell

## VNets

- Netzwerk in der Cloud
- kann in Subnetze unterteilt werden
- Default koennen alle Subnetze im VNet miteinander kommunizieren
- verweigern der kommunikation ueber NSGs

>[!note]
>Das kleinste Subnetz das supportet wird ist /29 und das groesste ist /2. 

## Planen eines IP Schemas 

- Anforderungen
	- Wie viele Geraete sollen in das Netzwerk?
	- Wie viele Geraete sollen in der Zukunft zum Netzwerk hinzugefuegt werden
- Welche Geräte müssen Sie basierend auf den in der Infrastruktur ausgeführten Diensten trennen? 
- Wie viele Subnetze benötigen Sie? 
- Wie viele Geräte pro Subnetz werden Sie haben?
- Wie viele Geräte planen Sie in Zukunft zu den Subnetzen hinzuzufügen? 
- Werden alle Subnetze gleich groß sein? 
- Wie viele Subnetze möchten oder planen Sie in Zukunft hinzuzufügen?