# Azure Speicherdienste

## Azure-Speicherkonto

Ein Speicherkonto stellt einen eindeutigen Namespace für Ihre Azure Storage-Daten bereit, auf den von überall auf der Welt per HTTP oder HTTPS zugegriffen werden kann.

### Speicherkontotypen

Der Kontotyp bestimmt die Speicherdienste und Redundanzoptionen und hat Auswirkungen auf die Anwendungsfälle

Redundanzoptionen:
- Lokal redundanter Speicher (LRS)
- Georedundanter Speicher (GRS)
- Georedundanter Speicher mit Lesezugriff (RA-GRS)
- Zonenredundanter Speicher (ZRS)
- Geozonenredundanter Speicher (GZRS)
- Geozonenredundanter Speicher mit Lesezugriff (RA-GZRS)

| Typ                     | Unterstuetzte Dienste                                                                          | Redundanzoptionen                    | Verwendung                                                                                                                                                                                                                 |
| ----------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Standard "Allgemein v2" | Blob Storage (einschliesslich Date Lake Storage), Queue Storage, Table Storage und Azure files | LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS | Standard-Speicherkontotyp. Empfohlen fuer die meisten Azure Storage Szenarien.                                                                                                                                             |
| Premium Blockblobs      | Blob Storage (einschliesslich Data Lake Storage)                                               | LRS, ZRS                             | für Block- und Anfügeblobs. Empfohlen für Szenarien mit hohen Transaktionsraten, die kleinere Objekte verwenden oder aber eine gleichbleibend geringe Speicherlatenz erfordern.                                            |
| Premium Dateifreigaben  | Azure Files                                                                                    | LRS, ZRS                             | nur für Dateifreigaben. Empfohlen für Unternehmens- oder Hochleistungsanwendungen. Verwenden Sie diesen Kontotyp, wenn Ihr Speicherkonto sowohl SMB- (Server Message Block) als auch NFS-Dateifreigaben unterstützen soll. |
| Premium Seitenblobs     | Nur Seiten-BLOBs                                                                               | LRS                                  | nur für Seitenblobs                                                                                                                                                                                                        |

### Speicherkontoendpunkte

- Speicherkonto benoetigt eindeutigen Kontonamen
- Kontoname + Azure Storage-Dienstpunkt bildet die Endpunkte fuer ihr Speicherkonto

Regeln bei der Benennung:

- zwischen 3 und 24 Zeichen lang sein und dürfen nur Zahlen und Kleinbuchstaben enthalten
- muss innerhalb von Azure eindeutig sein

#### Endpunktformate

| Speicherdienst         | Endpunkt                                              |
| ---------------------- | ----------------------------------------------------- |
| Blob Storage           | https://<storage-account-name>.blob.core.windows.net  |
| Data Lake Storage Gen2 | https://<storage-account-name>.dfs.core.windows.net   |
| Azure Files            | https://<storage-account-name>.file.core.windows.net  |
| Queue Storage          | https://<storage-account-name>.queue.core.windows.net |
| Table Storage          | https://<storage-account-name>.table.core.windows.net | 

## Azure Storage Redundanz

- speichert immer mehrere Kopien der Daten
- lokal redundanten Speicher (LRS) und dem zonenredundanten Speicher (ZRS) sind zwei Optionen für die Replikation der Daten in der primären Region

### Lokal redundanter Speicher (LRS)

- Daten innerhalb eines einzelnen Rechenzentrums in der primären Region repliziert
- bietet eine Dauerhaftigkeit von mindestens elf Neunen (99,999999999 Prozent)
- kostengünstigste Redundanzoption und bietet im Vergleich zu anderen Optionen die geringste Dauerhaftigkeit
- schützt Daten vor Serverrack- und Laufwerkfehlern

![[Azure_LRS.png]]

### Zonenredundanter Speicher (ZRS)

- repliziert Azure Storage-Daten synchron in drei Azure-Verfügbarkeitszonen in der primären Region
- bietet eine Dauerhaftigkeit von mindestens zwölf Neunen (99,9999999999 %)
- keine Neueinbindung von Azure-Dateifreigaben auf den verbundenen Clients erforderlich
- Empfehlung fuer High Availability

![[Azure_ZRS.png]]

### Georedundanter Speicher (GRS)

- erstellt mit LRS drei synchrone Kopien Ihrer Daten in primären Region
- Daten werden mithilfe des LRS asynchron an die sekundären Region (Regionspaar) kopiert
- bietet eine Dauerhaftigkeit von mindestens 16 Neunen (99,99999999999999 %)

![[Azure_GRS.png]]

### Geozonenredundanter Speicher (GZRS)

- kombiniert die Hochverfügbarkeit durch die verfügbarkeitszonenübergreifende Redundanz mit dem Schutz vor regionalen Ausfällen, der durch die Georeplikation geboten wird
- werden über drei Azure-Verfügbarkeitszonen in die primäre Region kopiert (wie ZRS)
- zum Schutz vor regionalen Notfällen mithilfe des LRS auch in eine sekundäre geografische Region repliziert
- Dauerhaftigkeit von mindestens 16 Neunen (99,99999999999999 %)
- Regonenuebergreifend nur Read-Only wenn Failover abgeschlossen
- Wenn Daten in sekundaerer Region immer lesbar sein sollen --> RA-GRS und RA-GZRS

![[Azure_GZRS.png]]

## Azure-Speicherdienste

- Azure-Blobs
	- skalierbarer Objektspeicher für Text- und Binärdaten
	- verfügt über Unterstützung für Big Data-Analysen mit Data Lake Storage Gen2
- Azure Files
	- Verwaltete Dateifreigaben für Bereitstellungen lokal oder in der Cloud
- Azure-Warteschlangen
	- Ein Messagingspeicher für zuverlässiges Messaging zwischen Anwendungskomponenten
- Azure-Datenträger
	- Speichervolumes auf Blockebene für virtuelle Azure-Computer
- Azure Tables
	- NoSQL-Tabellenoption für strukturierte, nicht relationale Daten

Vorteile von Azure Storage:

- Robust und Hochverfuegbar durch Redundanz
- Sicher durch Verschluesselung
- Skalierbar
- Verwaltet
- Zugaenglich ueber HTTP/HTTPS und Clientbibliotheken

### Azure Blobs

- kann große Mengen an Daten wie etwa Text- und Binärdaten speichern
- ist unstrukturiert, was bedeutet, dass es keine Einschränkungen hinsichtlich der Art der Daten gibt, die dort gespeichert werden können
- nicht auf gängige Dateiformate beschränkt
- Vorteil des Blobdiensts gegenüber des Datenträgerspeichers ist, dass Entwickler nicht darüber nachdenken oder Datenträger verwalten müssen

Fuer folgende Zwecke Ideal:

- Speichern von Bildern oder Dokumenten direkt für einen Browser
- Speichern von Dateien für verteilten Zugriff
- Video- und Audio-Streaming
- Speichern von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung
- Speichern von Daten für Analysen durch einen lokalen oder von Azure gehosteten Dienst

#### Zugriff auf Blobspeicher

- HTTP/HTTPS
- URLs
- Azure Storage REST API
- Azure CLI
- Azure Client Bibliothek

#### Blobspeicherebenen

- Hot Area
	- Optimiert fuer Daten mit haeufigem Zugriff
- Cold Area
	- Optimiert fuer Daten mit seltenerm Zugriff + mind. 30 Tage Gespeichert werden
- Access Area Cold
	- Optimiert fuer Daten mit seltenerm Zugriff + mind. 90 Tage Gespeichert werden
- Archive Area
	- seltener zugriff und die bei flexiblen Latenzanforderungen mindestens 180 Tage lang gespeichert werden


- Hot und Cold Area koennen uber Kontoebene festgelegt werden
- Zugriffsebene kann  waehrend des Uploads festgelegt werden
- Archive speichert Daten offline 
- Bei der Area Cold koennen High Availability abstriche gemacht werden koennen

### Azure Files

- bietet vollständig verwaltete Dateifreigaben in der Cloud
- laeuft ueber SMB oder NFS

#### Vorteile

- Gemeinsamer Zugriff
	- lokalen Dateifreigaben problemlos durch Azure-Dateifreigaben ersetzen
- Vollstaendig verwaltet
	- Hardware und OS verwaltung wird von Azure uebernommen 
- Skripts und Tools
	- PowerShell-Cmdlets und die Azure CLI können im Rahmen der Verwaltung von Azure-Anwendungen zum Erstellen, Bereitstellen und Verwalten von Azure-Dateifreigaben verwendet werden
- Resilienz
	- High Availability durch Cloud approach
- Vertraute Programmierbarkeit
	- Anwendungen können über Dateisystem-E/A-APIs auf Daten in der Freigabe zugreifen
	- Auch mit Clientlibraries und REST-API moeglich

### Azure-Warteschlangen

- Speicherung einer großen Anzahl von Nachrichten
- Aufrufen ueber HTTP/HTTPS
- 64KB max. groesse pro Message
- Kann mit Berechnungsfunktionen verbunden werden

### Azure-Disks

- sind Speichervolumes auf Blockebene
- werden von Azure-VMs als Speicherebene benutzt
- gleichen einem physischen Datenträger, aber sind virtualisiert und bieten so eine höhere Ausfallsicherheit und Verfügbarkeit

### Azure-Tabellen

- Speicherung strukturierter Daten
- NoSQL-Datenspeicher, der authentifizierte Aufrufe von innerhalb und außerhalb der Azure-Cloud akzeptiert

## Azure Datenmigration

### Azure Migrate

- Vereinheitlichte Migrationsplattform
	- Ein einzelnes Portal zum Starten, Ausführen und Nachverfolgen Ihrer Migration zu Azure
- Verfügbare Tools
	- Eine Reihe von Tools für Bewertung und Migration
	- Azure Migrate: Ermittlung und Bewertung
	- Azure Migrate: Servermigration
	- Azure Migrate kann auch in andere Azure-Dienste und -Tools sowie Angebote von unabhängigen Softwareanbietern (Independent Software Vendors, ISVs) integriert werden.
- Bewertung und Migration
	- Azure Migrate-Hub kann lokale Infrastruktur bewerten und zu Azure migrieren.

Integrierte Tools:

- Azure Migrate: Ermittlung und Bewertung
	- Als Vorbereitung für die Migration zu Azure werden lokale Server ermittelt und bewertet, die unter VMware, Hyper-V und auf physischen Servern ausgeführt werden
- Azure Migrate: Servermigration
	- VMware-VMs, Hyper-V-VMs, physische Server und andere virtualisierte Server und VMs der öffentlichen Cloud werden zu Azure migriert
- Datenmigrations-Assistent
	- eigenständiges Tool zur Bewertung von SQL Server-Instanzen
	- ermöglicht die Ermittlung möglicher Probleme, die einer Migration im Wege stehen können
	- identifiziert nicht unterstützte Features, neue Features
	- ermittelt den richtigen Pfad für die Datenbankmigration
- Azure Database Migration Service
	- Migrieren von lokalen Datenbanken zu Azure-VMs, auf denen SQL Server, Azure SQL-Datenbank oder verwaltete Azure SQL-Instanzen ausgeführt werden
- Azure App Service-Migrationsassistent
	- eigenständiges Tool, mit dem lokale Websites für die Migration zu Azure App Service bewertet werden können
	- zum Migrieren von .NET- und PHP-Web-Apps zu Azure
- Azure Data Box
	- Verschieben Sie große Mengen an Offlinedaten mit Azure Data Box-Produkten zu Azure

### Azure Data Box

- physischer Migrationsdienst
- Bereitstellung eines proprietären Data Box-Speichergeräts mit einer maximal nutzbaren Speicherkapazität von 80 Terabyte beschleunigt
- Transport des Data Box-Geräts von und zu einem Rechenzentrum erfolgt über einen regionalen Spediteur
- robustes Gehäuse schützt das Data Box-Gerät vor Transportschäden

## Azure Datenverschiebungsoptionen

### AzCopy

- ist ein Befehlszeilenprogramm zum Kopieren von Blobs oder Dateien in ein oder aus einem Speicherkonto
- kann Dateien hochladen, herunterladen, zwischen Speicherkonten kopieren und synchronisieren

### Azure Storage-Explorer

- eigenständige App mit einer Benutzeroberfläche zum Verwalten von Dateien und Blobs in Ihrem Azure Storage-Konto

### Azure-Dateisynchronisierung

- Tool zur Zentralisierung von Dateifreigaben in Azure Files bei gleichzeitiger Flexibilität, Leistung und Kompatibilität eines Windows-Dateiservers
- Nach Installation erfolgt automatisch eine permanente bidirektionale Synchronisierung mit Dateien in Azure

#### Vorteile 

- mit beliebigen Protokoll auf Daten zugreifen
- weltweit so viele Caches wie nötig nutzen
- fehlerhaften lokalen Server ersetzen, indem die Azure-Dateisynchronisierung auf einem neuen Server im gleichen Rechenzentrum installiert wird
- Cloudtiering konfigurieren, damit Dateien, auf die am häufigsten zugegriffen wird, lokal repliziert werden, während selten genutzte Dateien in der Cloud bleiben, bis sie angefordert werden
