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

## Verleich von Active Directory Domain Services (AD DS) mit Entra ID

Active Directory Domain Services (AD DS) ist die herkömmliche Bereitstellung einer Windows Server-basierten Active Directory-Instanz auf einem physischen oder virtuellen Server

### AD DS vs Entra ID

- Entra ID ist kein AD fuer die Cloud
- AD spricht kerberos aber Entra ID **nicht**
- AD ist primaer ein Verzeichnis und Entra ID ist eine volle Identitaets Loesung

Identitäts- und Zugriffsverwaltung
für Microsoft 365-Apps

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