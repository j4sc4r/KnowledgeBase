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
