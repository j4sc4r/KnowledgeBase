# Konfigurieren von Azure-Ressourcen mit Tools

## Azure Portal 

- Durchsuchen von Ressourcen, Diensten und Dokumentation
- Verwalten von Ressourcen
- Erstellen benutzerdefinierter Dashboards und Favoriten
- Zugreifen auf die Cloud Shell
- Empfangen von Benachrichtigungen
- Links zur Azure-Dokumentation

## Azure Cloud Shell 

- Ist temporär und setzt das Einbinden einer neuen oder vorhandenen Azure Files-Freigabe voraus
- Bietet einen integrierten grafischen Text-Editor, der auf dem Open-Source-Monaco-Editor basiert
- Authentifiziert sich automatisch für den sofortigen Zugriff auf Ihre Ressourcen.
- Wird auf einem temporären Host ausgeführt, der pro Sitzung und pro Benutzer bereitgestellt wird
- Nach 20 Minuten ohne interaktive Aktivitäten tritt ein Timeout ein
- Erfordert eine Ressourcengruppe, ein Speicherkonto und eine Azure-Dateifreigabe
- Verwendet dieselbe Azure-Dateifreigabe für Bash und PowerShell
- Wird einem Computer pro Benutzerkonto zugewiesen
- Stellt $HOME dauerhaft unter Verwendung eines 5-GB-Images bereit, das sich in Ihrer Dateifreigabe befindet
- Berechtigungen werden als normaler Linux-Benutzer in Bash festgelegt


## Azure PowerShell

- modul was der Windows PowerShell hinzugefuegt wird um Azure Commands ausfuehren zu koennen 
- Es kann folgende Azure-Ressourcen regulieren
	 - Ressourcengruppen
	- Speicher
	- VMs
	- Microsoft Entra ID
	- Container
	- Machine Learning


### Create a Resource Group in Azure PowerShell

- set  current location 
```powershell
$location = (Get-AzResourceGroup -Name <Name>).Location
```
- set resource group name
```powershell
$rgname = '<name>'
```
- create the resource group
```powershell 
New-AzResourceGroup -Name $rgname -Location $location
```

- Output

![[Azure_RG_PS.png]]

- show Resource Group
```powershell
Get-AzResourceGroup -Name $rgname
```

![[Azure_RG_PS_1.png]]

### Create a managed Disk 

- create the config 
```powershell 
$diskConfig = New-AzDiskConfig `
-Location $location `
-CreateOption Empty `
-DiskSizeGB 32 `
-Sku Standard_LRS
```
- set name of disk
```powershell
$diskName = '<Name>'
```
- create Disk
```powershell
New-AzDisk `
-RessourceGroupName $rgname `
-DiskName $diskName `
-Disk $diskConfig`
```
- Get properties of new Disk
```powershell
Get-AzDisk -ResourceGroupName $rgname -Name $diskName
```

### Increase size of Azure managed Disk

- update command
```powershell
New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgname -DiskName $diskName
```
- verificaiton command
```powershell
Get-AzDisk -ResourceGroupName $rgname -Name $diskName
```
- verify current SKU
```powershell
(Get-AzDisk -ResourceGroupName $rgname -Name $diskName).Sku
```
- output
![[Azure_Disk_update.png]]

- update to premium_LRS
```powershell
NewDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgname -DiskName $diskName
```


## Azure CLI

- ist ein Terminal was lokal laeuft 
- Befehle sind in Gruppen und Untergruppen strukturiert
- Befehle finden mit `az find`

### Restart a VM

```bash
az vm restart -g <ResourceGroup> -n <VmName>
```


### Create ResourceGroup with AzureCLI

- set location variable and resource group name
```bash
LOCATION=$(az group show --name '<name>' --query location --out tsv)

RGNAME=$('<ResourceGroupName>')
```
- creating the resource group
```bash
az grou create -n <Name> -l <Location> z.B. germanywestcentral>
```
- showing output
```bash
az group show -n <Name>
```

![[Azure_Bash.png]]

### Create a managed disk in the resource group

- creating disk
```bash
az disk create \
--resource-group <Resource group name> \
--name <DiskName> \
--sku <Replikationsoption z.B. Standard_LRS> \
--size-gb 32
```
- show disk 
```bash
az disk show -g <Resource group name> -g <DiskName>
```

### Update the managed disk size

- updating
```bash
az disk update -g <resource group name> -n <DiskName> --size-gb <amount>
```
- verification
```bash
az disk show -g <resource group name> -n <DiskName> --query diskSizeGB
```