# Azure Identitaeten, Zugriffe und Sicherheit

## Azure Verzeichnisdienste

**Microsoft Entra ID** ist ein Verzeichnisdienst zum anmelden und sowohl auf Microsoft-Cloudanwendungen als auch auf selbst entwickelte Cloudanwendungen zugreifen können.  

- kann als lokale Active Directory-Bereitstellung verwaltet werden
- cloudbasierte Identitäts- und Zugriffsverwaltungsdienst
- kann Anmeldeversuche von unerwarteten Standorten oder unbekannten Geräten erkennen

Wer verwendet Entra ID?

- IT-Administratoren
	- um den Zugriff auf Anwendungen und Ressourcen basierend auf ihren Geschäftsanforderungen zu steuern
- App-Entwickler
	- koennen standardbasierten Ansatz für das Hinzufügen von Funktionen zu den von ihnen entwickelten Anwendungen umsetzen
- Benutzer
	- können ihre Identitäten verwalten und Wartungsaktionen wie die Self-Service-Kennwortzurücksetzung ausführen
- Abonnent von Onlinediensten
	- Benutzer von Microsoft 365, Microsoft Office 365, Azure und Microsoft Dynamics CRM Online verwenden es bereits

### Was kann Microsoft Entra ID

- Authentifizierung 
	- Überprüfung der Identität für den Zugriff auf Anwendungen und Ressourcen
	- Funktionen wie Self-Service-Kennwortzurücksetzung
	- mehrstufige Authentifizierung
	- benutzerdefinierte Liste verbotener Kennwörter
	- intelligente Sperrdienste
- Einmaliges Anmelden
	- muss nur ein Benutzername und ein Kennwort gemerkt werden
	- Eine Identität an einen Benutzer gebunden, sodass das Sicherheitsmodell vereinfacht wird
	- Zugriffsänderungen an diese Identität gebunden
	- Aufwand für das Ändern oder Deaktivieren von Konten reduziert
- Anwendungsverwaltung
	- können Cloud- und lokale Apps verwalten
	- Mit Anwendungsproxies, SaaS-Apps, dem Portal „Meine Apps“ und dem einmaligen Anmelden wird die Benutzerfreundlichkeit verbessert
- Geraeteverwaltung
	- unterstützt die Registrierung von Konten für Einzelpersonen als auch von Geräten
	- Registrierung ermöglicht die Verwaltung von Geräten mithilfe von Tools wie Microsoft Intune
	- ermöglicht es gerätebasierten bedingten Zugriffsrichtlinien auch, Zugriffsversuche unabhängig vom anfordernden Benutzerkonto nur auf solche Versuche zu beschränken, die von bekannten Geräten stammen
- lokales AD und Entra ID koennen verknuepft werden
- Entra connect fuer Verknuepfung
- es synchronisiert Benutzeridentitäten zwischen lokalem Active Directory und Microsoft Entra ID

### Microsoft Entra Domain Service

- Dienst, der verwaltete Domaindienste wie Domainbeitritt, Gruppenrichtlinien, Lightweight Directory Access Protocol (LDAP) und Kerberos-/NTLM-Authentifizierung bereitstellt
- bietet den Vorteil, Domaindienste verwenden zu können, ohne Domaincontroller
- kann mit Ihrem vorhandenen Microsoft Entra-Mandanten integriert werden
- Nach erstellung festlegung eines eindeutigen Namespaces --> Domainname
- Anschliesend werden zwei Windows Server-Domänencontroller in ausgewählter Azure-Region bereitgestellt
- wird als Replikatgruppe bezeichnet
- Domaincontroller muss nicht verwaltet werden

Wie werden Informationen synchronisiert 

- verwaltete Domäne ist so konfiguriert, dass eine unidirektionale Synchronisierung von Microsoft Entra ID zu Microsoft Entra Domain Services erfolgt
- können Ressourcen direkt in der verwalteten Domäne erstellen, die aber nicht wieder mit Microsoft Entra ID synchronisieren
- In Hybridumgebungen mit lokaler AD DS-Umgebung synchronisiert Microsoft Entra Connect Identitätsinformationen mit Microsoft Entra ID, die mit der verwalteten Domäne synchronisiert werden

![[Azure_identity_access_security.png]]

## Azure Authentifizierungsmethoden

![[Azure_auth_security.png]]

### Single Sign-On (SSO)

- ermöglicht einmalige anmeldung und diese Anmeldeinformationen für den Zugriff auf mehrerer Ressourcen und Anwendungen von unterschiedlichen Anbietern zu verwenden
- muss sich nur eine Identitaet + PW gemerkt werden
- anwendungsübergreifende Zugriff wird einer einzigen Identität gewährt

### Multi-Factor-Authentication (MFA)

- hier wird nach einem zusätzlichen Formular zur Identifizierung während des Anmeldevorgangs gefragt
- bietet zusätzliche Sicherheit für Identitäten, indem mindestens zwei Methoden für eine vollständige Authentifizierung benötigt werden
- Beispiele sind Captcha-Frage, Code an privates Geraete wie Handy, biometrische Eigenschaften

### Passwordless Authentication (PA)

- sind bequemer, weil das Kennwort entfällt und durch etwas ersetzt wird was im privaten besitz ist oder biometrischer natur ist 

#### PA integrationen in Entra ID

- Windows Hello for Business
	- biometrische und PIN-basierte Anmeldeinformationen sind direkt mit dem PC des Benutzers verknüpft
	- Mit PKI-Integration (Public Key-Infrastruktur) und integrierter Unterstützung für einmaliges Anmelden fuer nahtlosen Zugriff in der Cloud
- Microsoft Authenticator-App
	- Smartphone als PA 
	- Koennen bei Anmeldungen informationen auf das Smartphone bekommen und mit PIN oder Biometrischen Eigenschaften sich verifizieren
- FIDO2-Sicherheitsschluessel
	- aktueller Standard, der den Webauthentifizierungsstandard (WebAuthn) beinhaltet
	- eine Phishing-resistente, standardbasierte Methode zur kennwortlosen Authentifizierung
	- man kann mit einem externen Sicherheitsschlüssel oder einem in ein Gerät integrierten Plattformschlüssel die anmeldungen durchfuehren
	- Handelt sich meist um USB-Geraete koennen aber auch Bluetooth oder NFC-Geraete sein
	- Hardwaregerät, das für die Authentifizierung sorgt, erhöht die Sicherheit eines Kontos

## Azure externe Identitaeten

![[Azure_AD_external_identities.png]]

### Funktionen

- B2B Collaboration (Business to Business)
	- moeglichkeit sich mit ihrer bevorzugten Identität bei Ihren Microsoft-Anwendungen oder anderen Unternehmensanwendungen anzumelden
	- Werden im Verzeichnis als Gastbenutzer angezeigt
- Direkte B2B-Verbindung
	- einrichtung von gegenseitigen bidirektionalen Vertrauensstellungen zu einer anderen Microsoft Entra-Organisation
	- unterstützt derzeit freigegebene Teams-Kanäle, sodass externe Benutzer in ihren eigenen Instanzen von Teams aus auf Ihre Ressourcen zugreifen können
	- werden im Verzeichnis nicht dargestellt, sind jedoch im freigegebenen Teams-Kanal sichtbar und können in Admin Center-Berichten für Teams überwacht werden
- Microsoft Azure Active Directory B2C (Business-to-Customer)
	- Bereitstellung der eigenentwickelten Apps

## Azure bedingter Zugriff

- ein Tool um Zugriff auf Ressourcen auf der Grundlage von Identitätssignalen zuzulassen oder zu verweigern
- Signale beinhalten, wer der Benutzer ist, wo sich der Benutzer befindet und von welchem Gerät der Benutzer Zugriff anfordert
- Befähigen von Benutzern, überall und jederzeit produktiv zu sein
- Schützen der Ressourcen der Organisation

![[Azure_bedingter_Zugriff.png]]

- Signal kann der Standort oder das Gerät des Benutzers sein bzw. die Anwendung, auf die er zugreifen möchte
- basierend auf Signalen wird entschieden welche Berechtigung bzw. welche Authentifizierung der Benutzer machen muss
- Danach wird die Entscheidung ausgefuehrt

## Azure rollenbasierte Zugriffsteuerung

- bietet integrierte Rollen, mit denen allgemeine Zugriffsregeln für Cloudressourcen beschrieben werden
- eigene Rollen koennen auch definiert werden
- jede Rolle verfügt über einen zugeordneten Satz von Zugriffsberechtigungen

![[Azure_RBAC.png]]

- RBAC wird für jede Aktion erzwungen, die für eine Azure-Ressource initiiert wird und den Azure Resource Manager durchläuft
- ist ein Verwaltungsdienst, der eine Möglichkeit bietet, Ihre Cloudressourcen zu organisieren und zu sichern
- RBAC erzwingt keine Zugriffsberechtigungen auf Anwendungs- oder Datenebene
- verwendet ein Zulassungsmodell
- Wenn eine Rolle zugewiesen wurde koennen im Geltungsberreich aktionen ausgefuehrt werden

## Zero-Trust-Modell

### Leitprinzipien

- Ausfuehrung einer explizieten Verifizierung
	- zur Authentifizierung und Autorisierung immer alle verfügbaren Datenpunkte heranziehen
- Verwendung vom Zugriff mit den geringsten Rechten
	- beschraenkung mit Just-In-Time- und Just-Enough-Access (JIT/JEA)
- Von Sicherheitsverletzungen ausgehen
	- minimierung von Auswirkungsradius und Segmentzugriff
	- ueberpruefung von End-to-End-Verschlüsselung
	- Nutzung von Analysen die Erkennung von Bedrohungen voranzutreiben und Abwehrmaßnahmen zu verbessern

### Anpassen von Zero Trust

- geht nicht davon aus, dass ein Geraet sicher ist nur weil es sich innerhalb des Unternehmensnetzwerks befindet
- **jeder muss** sich authentifizieren 
- basierend auf der Authentifizierung anstelle des Speicherorts wird Zugriff gewährt

![[Azure_Zero_Trust.png]]

## Defense-in-Depth

- soll Informationen schützen und Diebstahl durch Personen verhindern, die nicht zum Zugriff darauf berechtigt sind
- verwenden zahlreiche Mechanismen, um das Ausmaß von Angriffen abzudämpfen, durch die unberechtigter Zugriff auf Daten erlangt werden soll

### Schichten von Defense-in-Depth

- jede Ebene bietet Schutz 

![[Azure_DoD.png]]

- Physische Sicherheit
	- ist die erste Verteidigungslinie und schützt die Computinghardware im Rechenzentrum
- Identitaet und Zugriff
	- steuert den Zugriff auf die Infrastruktur und die Änderungssteuerung
- Umkreis
	- verwendet einen Schutz vor verteilten Denial-of-Service-Angriffen (DDoS), um umfangreiche Angriffe abzufangen, bevor diese einen Denial of Service für den Benutzer verursachen können
- Netzwerk
	- schränkt die Kommunikation zwischen Ressourcen durch Segmentierung und Zugriffssteuerung ein
- Compute
	- schützt den Zugriff auf virtuelle Computer
- Anwendung
	- stellt sicher, dass Anwendungen sicher sind und keine Sicherheitsrisiken aufweisen
- Daten
	- steuert den Zugriff auf Geschäfts- und Kundendaten, die Sie schützen müssen

## Microsoft Defender fuer Cloud

Ist ein Überwachungstool für die Verwaltung des Sicherheitsstatus und den Bedrohungsschutz.

### Schutz fuer jede Bereitstellung

- nativer Azure-Dienst ist so werden viele Azure-Dienste überwacht und geschützt
- automatische Bereitstellungen eines Log Analytics-Agent, um sicherheitsbezogene Daten zu sammeln im lokalen Rechenzentrum
- Bei Hybrid- und Multicloud wird mithilfe von Azure Arc und Nicht-Azure-Computer  der Defender ausgeweitet
- In der Cloud sind CSPM-Features (Cloud Security Posture Management) ohne Agent moeglich

### Nativer Azure-Schutz

- Azure-PaaS-Dienste
	- erkennt bedorhen die auf die PaaS Dienste abzielen
	- koennen Azure-Aktivitätsprotokolle auch mithilfe der nativen Integration in Microsoft Defender für Cloud Apps auf Anomalien untersuchen
- Azure-Datendienste
	- enthält Funktionen mit denen Daten automatisch in Azure SQL klassifizieren werden koennen
	- Bewertet potenzielle Sicherheitsrisiken für Azure SQL- und Storage-Dienste 
	- gibt Empfehlungen zu ihrer Entschärfung
- Netzwerke
	- es kann die Anfälligkeit für Brute-Force-Angriffe verringert werden
	- Zugriff auf VM-Ports einschränken, indem Sie den Just-In-Time-Zugriff auf VMs nutzen
	- Richtlinien fuer ausgewaehlte Ports

### Schutz von Hybridressourcen

- Funktionen zum Schutz fuer Nicht-Azure-Server
- erhaltung von maßgeschneiderte Bedrohungsdaten und priorisierte Warnmeldungen basierend auf Ihrer spezifischen Umgebung
- Azure Arc muss aktiviert sein

### Schutz vor Ressourcen aus anderen Clouds

- CSPM-Features 
	- bewertet Ihre AWS-Ressourcen gemäß AWS-spezifischen Sicherheitsempfehlungen und bezieht die Ergebnisse in Ihre Sicherheitsbewertung ein
	- Ressourcen werden auf Einhaltung integrierter AWS-spezifischer Standards (AWS CIS, AWS PCI-DSS und AWS Foundational Security Best Practices) bewertet
	- „Bestandsverzeichnis“ hilft AWS-Ressourcen zusammen mit Azure-Ressourcen zu verwalten
- Microsoft Defender for Containers
	- werden Containerbedrohungserkennung und erweiterten Schutzmaßnahmen auf Amazon EKS Linux-Cluster ausgeweitet
- Microsoft Defender for Servers
	- stattet Ihre Windows- und Linux-EC2-Instanzen mit Bedrohungserkennung und erweiterten Schutzmaßnahmen aus

### Bewerten, Schuetzen und Verteidigen

Microsoft Defender erfuellt wichtige Anforderungen wenn Sicherheit der Ressourcen und Workloads in der Cloud und lokal verwaltet werden.

- Kontinuierliche Bewertung
	- Kennen vom Sicherheitsstatus, Ermitteln und verfolgen von Sicherheitsrisiken
- Schuetzen
	- Härten der Ressourcen und Dienste mit dem Azure Security Benchmark
- Verteidigen
	- Erkennen und beheben von Bedrohungen für Ressourcen, Workloads und Dienste

![[Azure_BSV.png]]


#### Sicherheitswarnungen

- enthalten Details zu den betroffenen Ressourcen
- schlagen Korrekturschritte vor
- enthalten in manchen Fällen eine Option zum Auslösen einer Logik-App als Reaktion


