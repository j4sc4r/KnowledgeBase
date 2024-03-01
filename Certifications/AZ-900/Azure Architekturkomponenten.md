# Azure Architekturkomponenten

## Was ist Microsoft Azure

- Azure ist ein Portfolio mit Clouddiensten
- Anwendungen koennen mit Tools und Frameworks global Bereitgestellt werden

## Azure Konten

- Ist die erste Instanz um mit Azure zu Arbeiten
- Mit einem Azure Konto koennen mehrere Abonnements erstellt werden
- In den Abonnements werden die Ressourcen dediziert bereitgestellt

![[Azure_Konto.png]]


## Azure Zugriffsmodi

- Azure CLI Poweshell
- Azure CLI Bash
- Azure CLI Interactive
- Azure Portal

## Azure physische Infrastruktur

- Rechenzentren werden in Azure-Regionen und Azure-Verfuegbarkeitszonen gruppiert

### Azure-Regions

- geografischer Bereich auf der Erde
- mind. eins aber moeglicherweise mehr Rechenzentren mit low-latency Netzwerkverbindung
- einige Dienste stehen nur in einigen Regionen zur verfuegung

### Verfuergbarkeitszonen

- sind physich getrennte Rechenzentren in einer Azure-Region
- besteht aus mind. einem Rechenzentrum was unabhaengige Kuehlung, Netzwerk und Strom besitzt
- wenn eine Zone ausfaellt, arbeitet die andere dennoch weiter

![[Azure_Availibility_Zones.png]]

#### Verwendung von Verfuegbarkeitszonen in Apps

- Gedacht fuer Hochverfuegbarkeitsloesungen

Azure-Dienste, die Verfügbarkeitszonen unterstützen, können in drei Kategorien unterteilt werden:

- Zonale Dienste: Sie weisen die Ressource fest einer bestimmten Zone zu (z. B. virtuelle Computer, verwaltete Datenträger oder IP-Adressen).
- Zonenredundante Dienste: Die Plattform repliziert automatisch zonenübergreifend (z. B. zonenredundanter Speicher oder SQL-Datenbank).
- Nicht regionale Dienste: Dienste sind immer in Azure-Geografien verfügbar und sowohl gegen zonenweite als auch regionsweite Ausfälle resilient.

### Azure-Regionspaare

Azure-Regionen werden mit einer anderen Region, die mindestens 480 km entfernt ist, innerhalb derselben Geografie (z. B. USA, Europa oder Asien) kombiniert.

Vorteile: 
- Ermoeglicht Replikationen von Ressourcen innerhalb einer Geografie
- gleichzeitige Verringerung der Wahrscheinlichkeit das Naturkatastrophen oder Stromausfaelle eine gesamte Region treffen
- automatischen Failover von dem einen Regionspaar zum anderen (Muss vom Kunden konfiguriert werden)

![[Azure_Region_Pair.png]]

Weitere Vorteile:
- Bei umfrangreichen Ausfall wird ein paar Priorisiert um die Ressourcen schnellstmoeglich online zu bringen
- Azure-Updates werden nacheinander in den Regionspaaren installiert um ausfallsicherheit zu gewaehrleisten
- Die Daten bleiben aus steuerlichen und rechtlichen Gründen innerhalb derselben Geografie wie ihr Paar (mit Ausnahme von „Brasilien, Süden“).

Die meisten Regionen sind in zwei Richtungen gekoppelt. Zum Beispiel sichert US East, US West und auch umgekehrt. Einige Regionen werden aber auch nur in eine Richtung gesichert.

### Unabhaengige Regionen

- Azure hat auch unabhaengige Regionen
- Sind von der Haup-Azure-Instanz isoliert 
- Werden fuer Compliance- oder rechtliche Zwecke benutzt

## Azure Verwaltungsinfrastruktur

Die Verwaltungsinfrastruktur umfasst Azure-Ressourcen sowie Ressourcengruppen, Abonnements und Konten.

### Azure-Ressourcen und -Ressourcengruppen

Azure Ressourcen sind alles was bereitgestellt wird wie z.B. VMs, virtuelle Netzwerke und Datenbanken. 

Ressourcengruppen sind einfach nur Gruppierungen von Ressourcen.

![[Azure_Resource_Group.png]]

- Wenn eine Ressource erstellt wird muss diese in eine Ressourcengruppe platziert werden
- Eine Ressourcengruppe kann viele Ressourcen enthalten, aber eine einzelne Ressource kann jeweils nur in einer Ressourcengruppe enthalten sein
-  Ressourcengruppen koennen nicht geschachtelt werden
-  Wenn eine Aktion auf eine Ressourcengruppe angewendet wird, wird diese Aktion für alle Ressourcen innerhalb der Ressourcengruppe ausgeführt
- Wenn eine Ressourcengruppe geloescht wird, wird der komplette Inhalt geloescht
- Wenn Sie Zugriff auf eine Ressourcengruppe erteilen oder verweigern, steuern Sie damit den Zugriff auf alle Ressourcen innerhalb der Ressourcengruppe

### Azure-Abonnements

- Bietet authentifizierten und autorisierten Zugriff auf Azure-Produkte
- Ermöglicht die Bereitstellung von Ressourcen
- Verweist auf ein Azure-Konto bei dem es sich um eine Identität in Microsoft Entra ID oder einem Verzeichnis handelt, dem Microsoft Entra ID vertraut

![[Azure_Subscription.png]]

- Ein Konto kann mehrere Abonnements umfassen
	- Es koennen mehrere Abrechnungsmodelle und Zugriffsverwaltungsrichtlinien konfiguriert werden
- koennen Grenzen fuer Produkte, Dienste und Ressourcen definiert werden

Es gibt zwei Arten von Abonnementgrenzen:
- Abrechungsgrenzen
	- wird bestimmt, wie die Nutzung von Azure einem Azure-Konto in Rechnung gestellt wird
	- mehrere Abonnements fuer verschiedene Arten von Abrechungsanforderungen
	- separate Abrechungsberichte und Rechnungen pro Abo
- Zugriffssteuerungsgrenzen
	- Es koennen separate Abos fuer verschiedene Organisationsstrukturen erstellt werden
	- Innerhalb des Unternehmens koennen unterschiedliche Abteilungen bestimmte Abonnementsrichtlinien zugewiesen werden
	- können den Zugriff auf die Ressourcen, die Benutzer bereitstellen, mit spezifischen Abonnements verwalten und steuern

### Azure-Verwaltungsgruppen

- Stellen einen abonnementübergreifenden Bereich dar
- organisieren Abonnements in Containern und wenden Governancebedingungen an

![[Azure_Management_Groups.png]]

Abonnements innerhalb einer Verwaltungsgruppe erben automatisch die Bedingungen, die auf die Verwaltungsgruppe angewandt wurden, ebenso erben Ressourcengruppen die Einstellungen von Abonnements und Ressourcen die von Ressourcengruppen.

- 10.000 Verwaltungsgruppen werden pro Verzeichnis unterstuetzt
- Eine Verwaltungsgruppenstruktur unterstuetzt bis zu sechs Ebenen (Ohne Stamm- und Abonnementebene)
- Jede Verwaltungsgruppe und jedes Abonnement kann nur über ein übergeordnetes Element verfügen

