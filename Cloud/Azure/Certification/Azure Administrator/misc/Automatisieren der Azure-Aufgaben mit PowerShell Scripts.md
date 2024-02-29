# Automatisieren der Azure-Aufgaben mit PowerShell Scripts

## Installieren von PowerShell Az-Modul Windows

- Oeffnen der PowerShell 
```powershell
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery
```

- Wenn fehler dann ExecutionPolicy auf RemoteSigned setzen
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

- aktualisieren des PowerShell Moduls 
```powershell
Update-Module -Name Az
```

- Verbinden eines Azure Accounts
```powershell
Connect-AzAccount
```

- schauen welche Subscription akutell ausgewaehlt ist 
```powershell
Get-AzContext
```

- anzeigen aller verfuegbaren Subscriptions
```powershell
Get-AzSubscription
```

- aendern der aktuellen Subscription
```powershell
Set-AzContext -Subscription '<Name>'
```

- abrufen einer liste aller resource groups
```powershell
Get-AzResourceGroup

or 

Get-AzResourceGroup | Format-Table
```

- erstellen einer resource group
```powershell
New-AzResourceGroup -Name <name> -Location <location>
```

- ueberpruefung einer resource
```powershell
Get-AzResource

or 

Get-AzResource | Format-Table
```

- resource group filtern nach gruppenzugehoerigkeit
```powershell
Get-AzResource -ResourceGroupName <name>
```

- erstellen eines virtuellen computers
```powershell
New-AzVm
       -ResourceGroupName <resource group name>
       -Name <machine name>
       -Credential <credentials object>
       -Location <location>
       -Image <image name>
```

- Suffix AzVM use-cases

| Befehl         | Beschreibung                     |
| -------------- | -------------------------------- |
| `Remove-AzVM`  | Loescht eine Azure-VM            |
| `Start-AzVM`   | Startet eine beendete VM         |
| `Stop-AzVM`    | Beendet die ausfuehrung einer VM |
| `Restart-AzVM` | Startet eine VM neu              |
| `Update-AzVM`  | Aktualisiert die config einer VM |

- VMs in Subscriptions filtern
```powershell
Get-AzVM -Status

or 

Get-AzVM -Status -Name <name>
```

- updaten einer VM mit variablen
```powershell
$ResourceGroupName = "<name>"
$vm = Get-AzVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

### Uebungserstellung einer VM 

- Erstellung der VM 
```powershell
New-AzVM 
-Name testvm-westeurope-01 
-ResourceGroupName learn-2d49ae8b-d4db-455f-a7f3-3ba9ab59fa52 
-Location "West Europe" 
-Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest 
-Credential (Get-Credential) 
-OpenPorts 22 
-PublicIpAddressName "testvm-westeurope-01"
```

- VM-Objekt einer variablen zuordnen
```powershell
$vm = (Get-AzVM -Name "testvm-westeurope-01" -ResourceGroupName learn-2d49ae8b-d4db-455f-a7f3-3ba9ab59fa52)
```

- Output
![[Azure_testvm.png]]

- Spezielle Objekte werden mit `.` Notation aufgerufen
```powershell
$vm.HardwareProfile

or 

$vm.StorageProfile.OsDisk
```

- Aufrufen der Public IP
```powershell
Get-AzPublicIpAddress -Name "testvm-westeurope-01" -ResourceGroupName learn-2d49ae8b-d4db-455f-a7f3-3ba9ab59fa52
```

### Loeschen einer VM

- Stoppen der VM
```powershell
Stop-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName
```

- Entfernen der VM
```powershell
Remove-AzVM -Name $vm.Name -ResourceGroupName $vm.ResourceGroupName
```

- Auflistung der Resources in der Resource Group
```powershell
Get-AzResource -ResourceGroupName $vm.ResourceGroupName | Format-Table
```

- Loeschung der restlichen Resources von einer VM
```powershell
#Netzwerkschnittstelle
$vm | Remove-AzNetworkInterface -Force

#Datentraeger
Get-AzDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzDisk -Force

#Virtuelles Netzwerk
Get-AzVirtualNetwork -ResourceGroupName $vm.ResourceGroupName | Remove-AzVirtualNetwork -Force

#Netzwerksicherheitsgruppe
Get-AzNetworkSecurityGroup -ResourceGroupName $vm.ResourceGroupName | Remove-AzNetworkSecurityGroup -Force

#Public IP
Get-AzPublicIpAddress -ResourceGroupName $vm.ResourceGroupName | Remove-AzPublicIpAddress -Force
```

## Uebungserstellung einer VM mit PowerShell-Skript

```powershell
#Einfuegen der Eingabeparameter
param([sting]$resourceGroup)

#Aufforderung von Credentials
$adminCredential = Get-Credential -Message "<Message>"

#Schleifeninhalt fuer die erstellung von 3 VMs
For ($i = 1; $i -le 3; $i++)
{
	$vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
New-AzVM 
-ResourceGroupName $resourceGroup 
-Name $vmName 
-Credential $adminCredential 
-Image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest
}
```

- Ausfuehren des Skripts 
```powershell
./<path to script>
```

- Checken ob VMs angelegt wurden
```powershell
Get-AzResource -ResourceType Microsoft.Compute/virtualMachines
```
