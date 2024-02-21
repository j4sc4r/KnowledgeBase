# Azure Architekturkomponenten

## Was ist Microsoft Azure

Azure ist ein Portfolio mit Clouddiensten. Mit Azure können Sie Anwendungen in einem umfassenden globalen Netzwerk mit Ihren bevorzugten Tools und Frameworks erstellen, verwalten und bereitstellen.

## Azure Konten

- Ist die erste Instanz um mit Azure zu Arbeiten
- Mit einem Azure Konto kann man mehrere Abonnements beginnen und in diesen Abonnements die Ressourcen erstellen

![[Azure_Konto.png]]


## Azure Zugriffsmodi

- Azure CLI Poweshell
- Azure CLI Bash
- Azure CLI Interactive
- Azure Portal

## Azure physische Infrastruktur

- Azure Rechenzentren werden in Azure-Regionen und Azure-Verfuegbarkeitszonen gruppiert

### Azure-Regions

- geografischer Bereich auf der Erde
- mind. eins aber moeglicherweise mehr Rechenzentren die nicht weit voneinander entfernt und uber low-latency Netzwerk verbunden sind
- einige Dienste stehen nur in einigen Regionen zur verfuegung

### Verfuergbarkeitszonen

- sind physich getrennte Rechenzentren in einer Azure-Region
- besteht aus mind. einem Rechenzentrum was unabhaengige Kuehlung, Netzwerk und Strom besitzt
- wenn eine Zone ausfaellt, arbeitet die andere dennoch weiter

![[Azure_Availibility_Zones.png]]

#### Verwendung von Verfuegbarkeitszonen in Apps

- gedacht fuer Hochverfuegbarkeitsloesungen

Azure-Dienste, die Verfügbarkeitszonen unterstützen, können in drei Kategorien unterteilt werden:

- Zonale Dienste: Sie weisen die Ressource fest einer bestimmten Zone zu (z. B. virtuelle Computer, verwaltete Datenträger oder IP-Adressen).
- Zonenredundante Dienste: Die Plattform repliziert automatisch zonenübergreifend (z. B. zonenredundanter Speicher oder SQL-Datenbank).
- Nicht regionale Dienste: Dienste sind immer in Azure-Geografien verfügbar und sowohl gegen zonenweite als auch regionsweite Ausfälle resilient.

### Azure-Regionspaare

Azure-Regionen werden mit einer anderen Region, die mindestens 480 km (300 Meilen) entfernt ist, innerhalb derselben Geografie (z. B. USA, Europa oder Asien) kombiniert.

Vorteile: 
- Ermoeglicht Replikationen von Ressourcen innerhalb eienr Geografie
- gleichzeitige Verringerung der Wahrscheinlichkeit das Naturkatastrophen oder Stromausfaelle eine gesamte Region treffen
- automatischen Failover von dem einen Regionspaar zum anderen (Muss vom Kunden konfiguriert werden)

![[Azure_Region_Pair.png]]

Weitere Vorteile:
- Bei einem umfangreichen Ausfall von Azure wird eine Region aus jedem Paar priorisiert, um sicherzustellen, dass mindestens eine Region für Anwendungen, die in diesem Regionspaar gehostet werden, so schnell wie möglich wiederhergestellt wird.
- Geplante Azure-Updates werden nacheinander in den Regionen eines Paars eingeführt, um Ausfallzeiten und das Risiko von Anwendungsausfällen zu minimieren.
- Die Daten bleiben aus steuerlichen und rechtlichen Gründen innerhalb derselben Geografie wie ihr Paar (mit Ausnahme von „Brasilien, Süden“).

Die meisten Regionen sind in zwei Richtungen gekoppelt. Zum Beispiel sichert US East, US West und auch umgekehrt. Einige Regionen werden aber auch nur in eine Richtung gesichert.

### Unabhaengige Regionen

Neben den regulären Regionen verfügt Azure auch über unabhängige Regionen (Sovereign Regions). Unabhängige Regionen sind Instanzen von Azure, die von der Hauptinstanz von Azure isoliert sind. Unabhängige Regionen müssen Sie möglicherweise für Compliance- oder rechtliche Zwecke verwenden.

## Azure Verwaltungsinfrastruktur

Die Verwaltungsinfrastruktur umfasst Azure-Ressourcen sowie Ressourcengruppen, Abonnements und Konten.

### Azure-Ressourcen und -Ressourcengruppen

Azure Ressourcen ist alles was sie bereitstellen wie z.B. VMs, virtuelle Netzwerke und Datenbanken. 

Ressourcengruppen sind einfach nur Gruppierungen von Ressourcen.

![[Azure_Resource_Group.png]]

- Wenn eine Ressource erstellt wird muss diese in eine Ressourcengruppe platziert werden
- Eine Ressourcengruppe kann viele Ressourcen enthalten, aber eine einzelne Ressource kann jeweils nur in einer Ressourcengruppe enthalten sein
-  Ressourcengruppen koennen nicht geschachtelt werden
-  Wenn eine Aktion auf eine Ressourcengruppe angewendet wird, wird diese Aktion für alle Ressourcen innerhalb der Ressourcengruppe ausgeführt
- Wenn eine Ressourcengruppe geloescht wird, wird der komplette Inhalt geloescht
- Wenn Sie Zugriff auf eine Ressourcengruppe erteilen oder verweigern, steuern Sie damit den Zugriff auf alle Ressourcen innerhalb der Ressourcengruppe

### Azure-Abonnements

Ein Abonnement bietet authentifizierten und autorisierten Zugriff auf Azure-Produkte und -Dienste. Darüber hinaus ermöglicht es Ihnen die Bereitstellung von Ressourcen. Ein Azure-Abonnement verweist auf ein Azure-Konto, bei dem es sich um eine Identität in Microsoft Entra ID oder einem Verzeichnis handelt, dem Microsoft Entra ID vertraut.

![[Azure_Subscription.png]]

- Ein Konto kann mehrere Abonnements umfassen, es ist jedoch nur ein Konto erforderlich
- Koennen mehrere Abrechnungsmodelle und Zugriffsverwaltungsrichtlinien konfiguriert werden
- koennen Grenzen fuer Produkte, Dienste und Ressourcen definiert werden

Es gibt zwei Arten von Abonnementgrenzen zu Verfuegung:
- Abrechungsgrenzen
	- wird bestimmt, wie die Nutzung von Azure einem Azure-Konto in Rechnung gestellt wird
	- mehrere Abonnements fuer verschiedene Arten von Abrechungsanforderungen
	- separate Abrechungsberichte und Rechnungen pro Abo
- Zugriffssteuerungsgrenzen
	- Es koennen separate Abos fuer verschiedene Organisationsstrukturen erstellt werden
	- Innerhalb des Unternehmens koennen unterschiedliche Abteilungen bestimmte Abonnementsrichtlinien zugewiesen werden
	- können den Zugriff auf die Ressourcen, die Benutzer bereitstellen, mit spezifischen Abonnements verwalten und steuern

### Azure-Verwaltungsgruppen

Azure-Verwaltungsgruppen stellen einen abonnementübergreifenden Bereich dar. Sie organisieren Abonnements in Containern, die als Verwaltungsgruppen bezeichnet werden, und wenden Ihre Governancebedingungen auf die Verwaltungsgruppen an.

![[Azure_Management_Groups.png]]

- Abonnements innerhalb einer Verwaltungsgruppe erben automatisch die Bedingungen, die auf die Verwaltungsgruppe angewandt wurden, ebenso erben Ressourcengruppen die Einstellungen von Abonnements und Ressourcen die von Ressourcengruppen
- 10.000 Verwaltungsgruppen können in einem einzigen Verzeichnis unterstützt werden
- Eine Verwaltungsgruppenstruktur kann bis zu sechs Ebenen unterstützen. Hierbei werden die Stammebene und die Abonnementebene nicht mitgezählt
- Jede Verwaltungsgruppe und jedes Abonnement kann nur über ein übergeordnetes Element verfügen

