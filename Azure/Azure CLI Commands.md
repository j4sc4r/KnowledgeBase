# Azure CLI Commands

## Authentifizierung und Abonnementverwaltung

| Befehl           | Erklärung                                | Häufig verwendete Parameter                     |
| ---------------- | ---------------------------------------- | ----------------------------------------------- |
| `az login`       | Meldet den Benutzer bei Azure an.        | `--use-device-code`, `--username`, `--password` |
| `az account set` | Legt das zu verwendende Abonnement fest. | `--subscription`                                |

## Resourcenverwaltung

| Befehl            | Erklärung                                              | Häufig verwendete Parameter    | 
| ----------------- | ------------------------------------------------------ | ------------------------------ |
| `az group list`   | Listet alle Ressourcengruppen in Ihrem Abonnement auf. | `--query`, `--output`          |
| `az group delete` | Löscht eine Ressourcengruppe.                          | `--name`, `--yes`, `--no-wait` |

## Compute-Ressourcen (VMs)

| Befehl         | Erklärung                            | Häufig verwendete Parameter             |
| -------------- | ------------------------------------ | --------------------------------------- |
| `az vm create` | Erstellt eine virtuelle Maschine.    | `--resource-group`, `--name`, `--image` |
| `az vm update` | Aktualisiert Eigenschaften einer VM. | `--resource-group`, `--name`, `--set`   |
| `az vm delete` | Löscht eine spezifische VM.          | `--resource-group`, `--name`            |
| `az vm start`  | Startet eine gestoppte VM.           | `--resource-group`, `--name`            |
| `az vm stop`   | Stoppt eine laufende VM.             | `--resource-group`, `--name`            |
| `az vm resize` | Ändert die Größe einer VM.           | `--resource-group`, `--name`, `--size`  |

## Speicher- und Datenbankdienste

| Befehl                      | Erklärung                                        | Häufig verwendete Parameter                                     |
| --------------------------- | ------------------------------------------------ | --------------------------------------------------------------- |
| `az storage account create` | Erstellt ein Speicherkonto.                      | `--name`, `--resource-group`, `--location`, `--sku`             |
| `az storage account delete` | Löscht ein Speicherkonto.                        | `--name`, `--resource-group`                                    |
| `az sql db create`          | Erstellt eine neue Azure SQL-Datenbank.          | `--resource-group`, `--server`, `--name`, `--service-objective` |
| `az sql db delete`          | Löscht eine SQL-Datenbank.                       | `--name`, `--resource-group`, `--server`                        |
| `az cosmosdb create`        | Erstellt eine neue Azure Cosmos DB-Kontoinstanz. | `--name`, `--resource-group`, `--kind`                          |
| `az cosmosdb delete`        | Löscht eine Azure Cosmos DB-Kontoinstanz.        | `--name`, `--resource-group`                                    |

## Web- und Mobile-Apps

| Befehl                  | Erklärung                         | Häufig verwendete Parameter                                 |
| ----------------------- | --------------------------------- | ----------------------------------------------------------- |
| `az functionapp create` | Erstellt eine neue Function App.  | `--resource-group`, `--consumption-plan-location`, `--name` |
| `az webapp create`      | Erstellt eine neue Web-App.       | `--resource-group`, `--plan`, `--name`                      |
| `az functionapp delete` | Löscht eine Function App.         | `--name`, `--resource-group`                                |
| `az webapp delete`      | Löscht eine Web-App.              | `--name`, `--resource-group`                                |
| `az webapp stop`        | Hält eine Web-App an.             | `--name`, `--resource-group`                                |
| `az webapp start`       | Startet eine angehaltene Web-App. | `--name`, `--resource-group`                                |

## Identitaets- und Zugriffsmanagement

| Befehl              | Erklärung                                             | Häufig verwendete Parameter                             |
| ------------------- | ----------------------------------------------------- | ------------------------------------------------------- |
| `az ad user create` | Erstellt einen neuen Azure Active Directory Benutzer. | `--display-name`, `--password`, `--user-principal-name` |
| `az ad user delete` | Löscht einen Azure Active Directory Benutzer.         | `--id`                                                  |

## Netzwerkmanagement

| Befehl                        | Erklärung                                          | Häufig verwendete Parameter                              |
| ----------------------------- | -------------------------------------------------- | -------------------------------------------------------- |
| `az network vnet create`      | Erstellt ein virtuelles Netzwerk.                  | `--resource-group`, `--name`, `--address-prefix`         |
| `az network vnet delete`      | Löscht ein virtuelles Netzwerk.                    | `--name`, `--resource-group`                             |
| `az network vnet update`      | Aktualisiert ein virtuelles Netzwerk.              | `--name`, `--resource-group`, `--address-prefixes`       |
| `az network nic create`       | Erstellt eine Netzwerkschnittstelle (NIC).         | `--resource-group`, `--name`, `--vnet-name`, `--subnet`  |
| `az network nic delete`       | Löscht eine Netzwerkschnittstelle (NIC).           | `--name`, `--resource-group`                             |
| `az network nic update`       | Aktualisiert eine Netzwerkschnittstelle (NIC).     | `--name`, `--resource-group`, `--network-security-group` |
| `az network public-ip create` | Erstellt eine öffentliche IP-Adresse.              | `--resource-group`, `--name`, `--allocation-method`      |
| `az network public-ip delete` | Löscht eine öffentliche IP-Adresse.                | `--name`, `--resource-group`                             |
| `az network public-ip update` | Aktualisiert eine öffentliche IP-Adresse.          | `--name`, `--resource-group`, `--dns-name`               |
| `az network nsg create`       | Erstellt eine Netzwerksicherheitsgruppe (NSG).     | `--resource-group`, `--name`                             |
| `az network nsg delete`       | Löscht eine Netzwerksicherheitsgruppe (NSG).       | `--name`, `--resource-group`                             |
| `az network nsg update`       | Aktualisiert eine Netzwerksicherheitsgruppe (NSG). | `--name`, `--resource-group`, `--tags`                   |

## Azure Kubernetes Service (AKS)

| Befehl                   | Erklärung                                        | Häufig verwendete Parameter                                     |
| ------------------------ | ------------------------------------------------ | --------------------------------------------------------------- |
| `az aks create`          | Erstellt einen Azure Kubernetes Service Cluster. | `--resource-group`, `--name`, `--node-count`, `--enable-addons` |
| `az aks update`          | Aktualisiert einen AKS Cluster.                  | `--resource-group`, `--name`, `--enable-cluster-autoscaler`     |
| `az aks delete`          | Löscht einen AKS Cluster.                        | `--resource-group`, `--name`, `--yes`, `--no-wait`              |
| `az aks get-credentials` | Holt Zugangsdaten für einen AKS Cluster.         | `--resource-group`, `--name`                                    |

## Azure Container Instances (ACI)

| Befehl                | Erklärung                                   | Häufig verwendete Parameter             |
| --------------------- | ------------------------------------------- | --------------------------------------- |
| `az container create` | Erstellt einen Azure Container Instance.    | `--resource-group`, `--name`, `--image` |
| `az container delete` | Löscht eine Azure Container Instance.       | `--resource-group`, `--name`            |
| `az container update` | Aktualisiert eine Azure Container Instance. | `--resource-group`, `--name`, `--image` |

## Azure Managed Disks

| Befehl           | Erklärung                                   | Häufig verwendete Parameter                         |
| ---------------- | ------------------------------------------- | --------------------------------------------------- |
| `az disk create` | Erstellt einen verwalteten Datenträger.     | `--resource-group`, `--name`, `--size-gb`, `--zone` |
| `az disk delete` | Löscht einen verwalteten Datenträger.       | `--name`, `--resource-group`                        |
| `az disk update` | Aktualisiert einen verwalteten Datenträger. | `--name`, `--resource-group`, `--size-gb`           |

## Allgemeine Verwaltung und Monitoring

| Befehl                     | Erklärung                                          | Häufig verwendete Parameter                |
| -------------------------- | -------------------------------------------------- | ------------------------------------------ |
| `az monitor log-analytics` | Verwaltet Log Analytics Ressourcen.                | Verschiedene Parameter je nach Unterbefehl |
| `az policy assignment`     | Verwaltet Richtlinienzuweisungen.                  | `--policy`, `--scope`                      |
| `az role assignment`       | Verwaltet Rollenzuweisungen für Zugriffskontrolle. | `--role`, `--assignee`                     |