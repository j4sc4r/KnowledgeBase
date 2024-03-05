# AZ - 104 - 2 - Identities und Governance

[Was ist Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/whatis)

![[Azure_EntraID.png]]

[Entra ID devices](https://learn.microsoft.com/en-us/azure/active-directory/devices/overview)

# Microsoft Entra ID

[Microsoft Entra ID](https://learn.microsoft.com/de-de/azure/active-directory/) ist der mehrinstanzenfähige cloudbasierte Verzeichnis- und Identitätsverwaltungsdienst von Microsoft.

## Funktionen von Microsoft Entra ID

- Single Sign-On
	- auf Webapps in der Cloud und auf on-premise apps
- Umfassende Geraeteunterstuetzung fuer iOS, Windows, Android and MacOS
- Sicherer Remotezugriff
	- auf on-premise apps von ueberall
	- sicherer Zugriff
		- Multi Factor Auth
		- Richtlinien für bedingten Zugriff
		- gruppenbasierte Zugriffsverwaltung
- Clouderweiterbarkeit
	- einheitlicher Satz von Benutzern, Gruppen, Anmeldeinformationen und Geräten in verschiedenen Umgebungen
- Schutz vertraulicher Daten
- Self-Service-Support
- Benutzt REST-API Schnittstelle
	- HTTP/HTTPS Schnittstelle
		- OIDC
		- OAuth
		- SAML
## Entra ID Konzepte

- Identitaet
	- ist ein Objekt, das authentifiziert werden kann
	- kann ein User mit Kennwort
	- koennen auch Anwendungen oder andere Server sein
	- Authentifizierung über geheime Schlüssel oder Zertifikate
	- Entra ID ist das Produkt das den Identitätsdienst bereitstellt
- Konto
	- Identitaet der Daten zugeordnet sind
	- Kein Konto ohne Identitaet
- Microsoft Entra-Konto
	- ist eine ueber Entra ID erstellte Identität
	- Identitäten werden in Microsoft Entra ID gespeichert und sind für die Clouddienstabonnements Ihrer Organisation zugänglich
- Azure-Mandant (Verzeichnis/Tenant)
	- einzelne vertrauenswuerdige Instanz von Entra ID
	- jedes Mandant ist eigene Organisation
- Azure-Abonnement
	- jedes Abo bekommt eigenen Mandant
	- dient zur Bezahlung von Azure Diensten
	- mehrere Abos moeglich

## Vergleich von Active Directory Domain Services (AD DS) mit Entra ID

Active Directory Domain Services (AD DS) ist die herkömmliche Bereitstellung einer Windows Server-basierten Active Directory-Instanz auf einem physischen oder virtuellen Server

### AD DS vs Entra ID

- Entra ID ist kein AD fuer die Cloud
- AD spricht kerberos aber Entra ID **nicht**
- AD ist primaer ein Verzeichnis und Entra ID ist eine volle Identitaets Loesung

## Entra-Versionen

Was koennen die Versionen von Entra ID, was die freie Version nicht kann.

| Kostenlos | P1                                          | P2                                          | MS365                                       |
| --------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
|           | Identitaet und Zugriffsverwaltung fuer MS65 | Identitaet und Zugriffsverwaltung fuer MS65 | Identitaet und Zugriffsverwaltung fuer MS65 |
|           | Premium-Features                            | Premium-Features                            |                                             |
|           | Hybrididentitaeten                          | Hybrididentitaeten                          |                                             |
|           | Erweiterte Gruppenverwaltung                | Erweiterte Gruppenverwaltung                |                                             |
|           | Bedingter Zugriff                           | Bedingter Zugriff                           |                                             |
|           |                                             | Schutz der Identitaet                       |                                             |
|           |                                             | Identity Governance                         |                                             |

Ab Version P1 ist der Self-Service-Kennwortzurücksetzung (SSPR) inbegriffen.

# Benutzer und Gruppen

## Benutzer

- jeder Benutzer benoetigt ein Azure-Benutzerkonto
- 3 Arten: 
	- Cloudidentitaet
		- Entra ID definierter Cloud Benutzer und teiler der eigenen Organisation
	- Verzeichnissynchrone Identitaeten
		- Lokal AD DS definierter Benutzer die ueber Entra Connect mit der Cloud verbunden werden
	- Gastbenutzer
		- definition ausserhalb von Azure
		- koennen externe Anbieter oder Auftraggeber sein
- funktion fuer Massennutzer bereitstellung

## Gruppen

- 2 Arten von Gruppen:
	- Sicherheitsgruppe
		- Verwaltung von Zugriffen und Resource Freigaben
	- MS365-Gruppe
		- Zugriff auf MS365 Apps (Sharepoint, Outlook, usw.)
- 3 Arten von Gruppenzuweisungen:
	- Zugewiesen
		- Benutzer manuell der Gruppe zuweisen
	- Dynamischer Benutzer
		- automatisches hinzufuegen durch attribute des Users
	- Dynamisches Geraet
		- automatisches hinzufuegen durch attribute des Geraets

## Verwaltungsgruppen (Management Groups)

Verwaltungsgruppen sind die Schicht uber den Abonnements. Es koennen hier auch Policies und Zugriffssteuerung verwendet werden.
Abonnements erben die Policies und Zugriffsrechte der Verwaltungsgruppe.

### Bedenken bei der Benutzung von Verwaltungsgruppen

- benutzerdefinierte Hierarchien
- Vererbung von Richtlinien
	- Abonnements vererben Richtlinien
	- Begrenzung aller Ressourcen auf eine bestimmte Region
- Compliance-Regeln
- Kostenberichterstattung

# Abonnements (Subscriptions)

Azure-Abonnement ist eine logische Einheit von Azure-Diensten, die mit einem Azure-Konto verknüpft ist. 
Das Azurekonto ist eine Entra ID Identitaet oder ein Verzeichnis/Tenant was Entra ID vertrauenswuerdig ist. 

- Mehrere Abonnements können mit demselben Azure-Konto verknüpft werden.
- Mehrere Azure-Konten können mit demselben Abonnement verknüpft werden.
- Die Abrechnung für Azure-Dienste erfolgt auf Abonnementbasis.

# Microsoft Cost Management

**Tools:**
- Kostenanalyse
- Budgetoptionen
- Empfehlungen fuer Kosteneinsparung
- Exportieren von Kostendaten

# Resource Tags

Wird fuer die logische Kategorisierung von Azure-Resources benutzt.
Mit Tags kann sortiert, durchsucht, verwaltet und analysiert werden.

- maximal 50 Tagname-Wert-Paare pro Resource / Resource Group
- Tags werden nicht vererbt

# Azure Policy

| Vorteil                                  | Beschreibung                                                                                                                                                                                                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Erzwingen von Regeln und Compliance      | Aktiviere integrierte Richtlinien oder erstellen Sie benutzerdefinierte Richtlinien für alle Ressourcentypen.Unterstützt die Auswertung und Durchsetzung von Richtlinien in Echtzeit sowie regelmäßige oder On-Demand-Compliancebewertung        |
| Anwenden von Richtlinien im grossen Stil | Anwenden von Richtlinien auf eine Verwaltungsgruppe mit Kontrolle über die gesamte Organisation. Anwendung von mehreren Richtlinien, und aggregieren Sie Richtlinienzustände mit der Richtlinieninitiative. Definition eines Ausschlussbereiches |
| Durchfuehrung der Wartung                | Führen Sie die Wartung in Echtzeit und für vorhandene Ressourcen durch.                                                                                                                                                                          |
| Ausueben von Governance                  | Implementierung von Governanceaufgaben für Ihre Umgebung                                                                                                                                                                                         |

Richtliniendefinition --> Festlegung von Compliancebedingungen
Initiativendefinition --> Gruppierung von Richtliniendefinitionen

## 4 Schritte der Policy bereitstellung

- Definition einer Richtlinie erstellen
	 - bewertende Bedingung & auszuführende Aktion, wenn die Bedingung erfüllt ist
- Definition einer Initiative erstellen
	- eine Reihe von Richtliniendefinitionen zur Verfolgung des Status Ressourceneinhaltung, um ein größeres Ziel zu erreichen
- Umfang der Initiativendefinition
	- Bestimmte Management- oder Ressourcengruppen oder Abonnements
-   Bestimmung der Konformität

# Role-based-access-control (RBAC)

- auch rollenbasierte Zugriffskontrolle genannt

| Konzept              | Beschreibung                                                                                                                                                                                                                                                              | Beispiele                                                                                                      |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Sicherheitsprinzipal | Ein Objekt, das etwas darstellt, das Zugriff auf Ressourcen anfordert                                                                                                                                                                                                     | Benutzer, Gruppen, Dienstprinipal, verwaltete Identitaet                                                       |
| Rollendefinition     | Berechtigungssatz, der die zulässigen Vorgänge angibt. Gibt vordefinierte Rollen aber koennen auch benutzerdefinierte Rollen erstellt werden                                                                                                                              | Leser, Mitwirkender, Besitzer                                                                                  |
| Bereich              | Die Grenze für die angeforderte _Zugriffsstufe_, d. h., „wie viel“ Zugriff gewährt wird                                                                                                                                                                                   | Verwaltungsgruppe, Abonnement, Resourcen Gruppe, Resource                                                      |
| Abtretung            | Eine **Zuweisung** fügt eine **Rollendefinition** an einen **Sicherheitsprinzipal** innerhalb eines bestimmten **Bereichs** an. Benutzer können den in einer Rollendefinition beschriebenen Zugriff gewähren, indem sie eine Zuweisung für die Rolle erstellen (anfügen). | - Zuweisen der Rolle _Benutzerzugriffsadministrator_ zu einer Administratorengruppe in einer Verwaltungsgruppe | 

## Rollendefinitionen

- _Actions_-Berechtigungen geben an, welche Aktionen zulässig sind.
- _NotActions_-Berechtigungen geben an, welche Aktionen nicht zulässig sind.
- _DataActions_-Berechtigungen geben an, wie Daten geändert oder verwendet werden können.
- _AssignableScopes_-Berechtigungen geben die Bereiche an, in denen eine Rollendefinition zugewiesen werden kann.

### NotActions

- `Authorization/*/Delete` hebt die Berechtigung zum Löschen und Entfernen für „alle“ auf.
- `Authorization/*/Write` hebt die Berechtigung zum Schreiben und Ändern für „alle“ auf.
- `Authorization/elevateAccess/Action` hebt die Berechtigung zum Erweitern der Ebene oder des Umfangs von Zugriffsberechtigungen auf.

Die Rolle _Mitwirkender_ verfügt außerdem über zwei Berechtigungen, die angeben, wie Daten geändert werden können:

- `"NotDataActions": []`: Es werden keine spezifischen Aktionen aufgeführt. Daher können sich alle Aktionen auf die Daten auswirken.
- `"AssignableScopes": ["/"]`: Die Rolle kann für alle Bereiche zugewiesen werden, die Auswirkungen auf Daten haben. `{\}` wildcard means "all"

### Wissenswertes ueber Rollendefinitionen

- RBAC bietet integrierte Rollen
- Rolle _Besitzer_ verfügt über die umfassendsten Zugriffsberechtigungen
- _AssignableScopes_-Berechtigungen einer Rolle können Verwaltungsgruppen, Abonnements, Ressourcengruppen oder Ressourcen sein

## Geltungsbereiche von Rollen

- So machen Sie eine Rolle für die Zuweisung in zwei Abonnements verfügbar
```json
"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
```

- So machen Sie eine Rolle nur für die Zuweisung in der Netzwerkressourcengruppe verfügbar
```json
"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network"
```

- So machen Sie eine Rolle für die Zuweisung für alle Anforderer verfügbar
```json
"/"
```

## Azure RBAC roles vs Azure Entra ID roles

- RBAC verwaltet den Zugang zu Azure-Ressourcen, Entra ID verwaltet den Zugang zu Azure-Entra-Ressourcen.
- Der RBAC-Bereich hat mehrere Ebenen, wie Verwaltungsgruppen oder Abonnements. Entra ID wird auf Tenant-Ebene skaliert.
- RBAC-Rollen können über das Azure-Portal, Cli, Powershell, ARM Templates oder REST API definiert werden. Entra ID-Rollen: Azure-Admin-Portal, 365-Admin-Portal usw.