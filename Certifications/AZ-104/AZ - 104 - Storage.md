# AZ - 104 - Storage

# Storage account konfigurieren 

- Azure weit eindeutigen Name
- nur kleinbuchstaben und zahlen

## Speichertypen

- Virtuelle Computer daten
	- VM Datentraeger
	- Anzahl der Datentraeger haengt von der groesse der VM ab
	- max. kapazitaet eines Datentraegers ist 32.767GB
- Unstrukturierte Daten
	- wenigsten organisierten Datentypen
	- nicht strukturierte Daten
	- nicht relationale Daten
	- Azure Blob Storage
	- Azure Data Lake Storage
		- Hadoop Distributed File System as a service
- Strukturierte Daten
	- relationales Format
	- verfuegt ueber freigegebenes Schema
	- werden in Datenbanktabellen gespeichert mit 
		- Zeilen
		- Spalten
		- Schluesseln
	- Azure Table Storage
	- Azure CosmosDB
		- global verteilter Datenbankdienst
	- Azure SQL
		- vollständig verwaltete Database-as-a-Service-Lösung

## Speicherkontoebenen

- Standard 
	- Speicherkonten werden mit magnetischen Festplattenlaufwerken (HDD) gesichert
	- niedrigsten Kosten pro GB
	- Benutzt fuer Massenspeicherung auf die nur selten zugegriffen werden
- Premium
	- basieren auf SSD-Datenträgern (Solid State Drive)
	- für Azure-VM-Datenträger oder Datenbanken

>[!NOTE]
>Man kann nicht das Standardkonto zu einen Premiumkonto umwandeln und umgekehrt. 

## Speicherkontotypen

- Standard-Universell v2
	- Blobstorage (mit Data Lake Storage)
	- Queue Storage
	- Table Storage
	- Azure Files
	- Standardspeicherkonto fuer die meisten Szenarien
- Premium Blockblobs
	- Blobstorage (mit Data Lake Storage)
	- Fuer Anwendungen mit hohen Transaktionsraten
	- arbeiten mit kleineren Objekten oder konsistente niedrige Speicherlatenz
- Premium Dateifreigaben
	- Azure Files
	- Fuer Unternehmens und Hochleistungsanwendungen
	- Unterstuetzung fuer SMB und NFS Dateifreigaben
- Premium Seitenblobs
	- Nur Seiten-BLOBs
	- Hochleistungsspeicher nur für Seitenblobs
	- Speichern von Sparsedatenstrukturen und indexbasierten Datenstrukturen wie z. B. Betriebssysteme, Datenträger für VMs sowie Datenbanken

>[!NOTE]
>Alle Speicherkontotypen werden mit der Speicherdienstverschlüsselung (Storage Service Encryption, SSE) für ruhende Daten verschlüsselt.

## Storage-Dienste

- Azure Blob Storage (Container)
	- hochgradig skalierbarer Objektspeicher für Text- und Binärdaten
	- geeignet fuer Backup (Sicherung) und Restores (Wiederherstellung) 
	- geeignet fuer Video und Audio streaming
	- NFS Protokoll Zugriff
	- Zugriff von ueberall (HTTP/S, URL, API, CLI)
- Azure Files
	- Verwaltete Dateifreigaben
	- hochverfügbare Dateifreigaben im Netzwerk
	- SMB oder NFS Protokoll
	- Authentifizierung ueber Speicherkonto-Anmeldeinformationen
- Azure Queue Storage
	- wird zum Speichern und Abrufen von Nachrichten verwendet
	- max. 64KB pro Nachricht
- Azure Table Storage (Azure CosmosDB)
	- voll gemanagete noSQL Datenbank 
	- automatisches managing, updating und patching
	- automatisches scaling
- Disks

>[!Info] Azure Queue (Warteschlangenspeicher) Szenario:
>Erwägen Sie das Szenario, in dem Ihre Kunden in der Lage sein sollen, Bilder hochzuladen, und Sie für jedes Bild Miniaturansichten erstellen möchten. Sie können Kunden warten lassen, bis die Miniaturbilder beim Hochladen der Bilder erstellt werden. Eine Alternative besteht darin, eine Warteschlange zu verwenden. Wenn der Kunde den Upload abgeschlossen hat, können Sie eine Nachricht in die Warteschlange schreiben. Dann können Sie eine Azure-Funktion verwenden, um die Nachricht aus der Warteschlange abzurufen und die Miniaturansichten zu erstellen. Die einzelnen Verarbeitungsabschnitte können gesondert skaliert werden, was Ihre Kontrolle über die Optimierung der Konfiguration erhöht.

## Replikation 

- locally redundant storage (LRS)
	- repliziert im selben Rechenzentrum
- zone redundant (ZRS)
	- repliziert in mehreren Rechenzentren in der gleichen Region
- geo redundant (GRS)
	- repliziert in eine zweite Region
	- RA-GRS: basiert auf GRS aber mit 24/7 Lesenzugriff
	- Nur GRS --> nur Lesenzugriff von der zweiten Region, bei einem Ausfall
- geo-zone redundant storage (GZRS)
	- kombiniert ZRS und GRS
		- repliziert 3x in ZRS 
		- repliziert in eine sekundaere Region
	- gibt auch RA-GZRS

## Zugreifen auf Speicher

[!info] Jedes Objekt was gespeichert wird hat eine eindeutige URL Adresse.

`//`**`mystorageaccount`**`.blob.core.windows.net/`**`mycontainer`**`/`**`myblob`**.

Es koennen benutzerdefinierte Domains verwendet werden. 

Direkte zuordnung: 

- Direkte Zuordnung ermöglicht Aktivierung einer benutzerdefinierten Domäne für eine Unterdomäne zu einem Azure-Speicherkonto.
- Erfordert Erstellung eines CNAME-Eintrags, der die Unterdomäne auf das Azure-Speicherkonto verweist.

- Unterdomäne: `blobs.contoso.com`
- Azure-Speicherkonto: `\<storage account>\.blob.core.windows.net`
- Direkter `CNAME`-Eintrag: `contosoblobs.blob.core.windows.net`


Zuordnung einer zwischendomain:

- Anwenden einer Zwischendomäne auf eine in Azure genutzte Domäne kann zu Ausfallzeiten führen.
- Nutzung von "asverify" vor der eigenen Unterdomäne erlaubt Verifizierung ohne DNS-Änderung und ermöglicht Zuordnung zum Blob-Endpunkt ohne Ausfallzeit.

- `CNAME`-Eintrag: **`asverify`**`.blobs.contoso.com`
- `CNAME`-Zwischeneintrag: **`asverify`**`.contosoblobs.blob.core.windows.net`

# Azure Blob Storage 

Blob steht für „Binary Large Object“. Blob Storage wird auch als Objektspeicher oder Containerspeicher bezeichnet.

Azure Blob Storage ist ein Dienst für die Speicherung großer Mengen unstrukturierter Objektdaten. Unstrukturierte Daten sind Daten, die nicht einem bestimmten Datenmodell oder einer bestimmten Definition entsprechen, wie z. B. Text- oder Binärdaten.

- speichert jede Art von Text- und Binaerdateien
- verwendet drei Resourcen zum Speichern und Verwalten
	- Azure Speicherkonto
	- Container in einem Azure-Speicherkonto
	- Blobs in einem Container

Blob cannot exist by itself. Must be inside a container resource.

Azure account can have unlimited containers and containers can have unlimited blobs.

## Blob Storage Implementationsbeispiele

- Browseruploads
	- Verwenden Sie Blob Storage, um Bilder oder Dokumente direkt an einen Browser zu senden.
- verteilten Zugriff
	- Blob Storage kann Dateien für verteilten Zugriff speichern, z. B. während eines Installationsvorgangs.
- Streamen von Daten
	- Streamen Sie Video- und Audiodaten mithilfe von Blob Storage.
- Archivierung und Wiederherstellung
	- Blob Storage ist eine hervorragende Lösung für die Speicherung von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung.
- Anwendungszugriff
	- Sie können Daten in Blob Storage für die Analyse durch einen lokalen oder in Azure gehosteten Dienst speichern.

## Blob Zugriff

- **Privat**: (Standard) Verbieten des anonymen Zugriffs auf den Container und Blobs.
- **Blob**: Zulassen des anonymen öffentlichen Lesezugriffs nur auf Blobs.
- **Container**: Zulassen des anonymen öffentlichen Lese- und Auflistungszugriffs auf den gesamten Container einschließlich der Blobs.

## Blobzugriffsebene

- Heisse Zugriffsebene (Hot)
	- haeufige Lese- und Schreibvorgaenge
	- niedrige Zugriffskosten, hoehere Speicherkosten
- Kalte Zugriffsebene (Cool)
	- Datenspeicherung fuer seltenen Zugriff
	- mind. 30 Tage lang gespeichert
- Ebene "Cold" (Cold)
	- langzeitspeicherung von grossen Datenmengen
	- mind. 90 Tage lang gespeichert
- Archivzugriffsebene (Archiv)
	- offline speicher fuer archivierte Datensaetze
	- mindestes 180 Tage lang gespeichert

## Lifecycle Regeln fuer Blobs

Sie können Regeln mit If-Then-Clauses aufstellen.

Wenn der Blob älter als 30 Tage ist, in den Archivspeicher verschieben. Wenn Blob älter als 100 Tage, Blob löschen.

## Blob objekt replikation

asynchrone Replikation von Containern über Regionen hinweg

- erfordert die Aktivierung der Versionierung in Quelle und Ziel
- Unterstützt keine Snapshots
- nur für Hot und Cool Tiers

## Blobtypen

- Blockblobs
	- Datenblöcke, die zu einem Blob zusammengefügt werden
	- die meisten Szenarien verwenden Block-Blobs
	- ideal für Text- und Binärdaten: Dateien, Bilder, Videos
- Anfuegeblobs (append)
	- ähnlich wie ein Block, optimiert für das Anhängen
	- nützlich für Protokollierungsszenarien
- Seitenblobs (page)
	- bis zu 8tb groß
	- effizient für häufige Lese-/Schreibvorgänge
	- Virtuelle Azure-Maschinen verwenden Page-Blobs für Betriebssystem- und Datenfestplatten

## Upload Tools

- AzCopy
	- CLI Tool fuer Windows und Linux
- Azure Data Factory

## Storage sicherheit 

### Shared Access Signatures (SAS)

SAS stellt eine sichere Methode zur Freigabe Ihrer Speicherressourcen dar, ohne dass Sie Kompromisse bei der Sicherheit der Kontoschlüssel eingehen müssen.

Gewaehrt Zugriff auf eine Resource fuer einen bestimmten Zeitraum. 

- granulare Kontrolle
- kann Zugriff auf mehrere Azure Storage Dienste gewaehren: Blobs, Files, Tables
- kann Zeitintervall und Ablauf festlegen
- kann Berechtigungen festlegen

### Verschluesselung

Die Azure Storage-Verschlüsselung ist für alle neuen und bestehenden Speicherkonten aktiviert und kann nicht deaktiviert werden.