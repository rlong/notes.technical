

Dump permissions for a file or folder
=====================================

cut down from [Script PowerShell: NTFS Permission Auditor For Folders and Files](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-NTFS-Permission-59c03872)

```
[CmdletBinding()]
Param (
	[Parameter(Mandatory=$True,Position=0)]
	[String]$AccessItem
)

If (!(Test-Path $AccessItem)) {
	Write-Host
	Write-Host "`t Item $AccessItem Not Found." -ForegroundColor "Yellow"
	Write-Host
}
Else {
	Write-Host
	Write-Host "`t Working. Please wait ... " -ForegroundColor "Yellow"
	Write-Host
	If((Get-Item $AccessItem).PSIsContainer -EQ $True) {
		Write-Host  "ItemType: Folder"
	}
	Else {
		Write-Host  "ItemType: File"
	}
	$Owner = (Get-Item -LiteralPath $AccessItem).GetAccessControl() | Select Owner
	$Owner = $($Owner.Owner)
	Write-Host "Owner: $Owner"
    (Get-Item -LiteralPath $AccessItem).GetAccessControl() | Select * -Expand Access | Select IdentityReference, FileSystemRights, AccessControlType, IsInherited, InheritanceFlags, PropagationFlags 
}
```

