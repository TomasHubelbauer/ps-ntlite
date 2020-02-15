# PowerShell NTLite

Downloads the NTLite installer and extracts `NTLite.exe` from it, cleaning up after itself.

Depends on [`inno.ps1`](https://github.com/TomasHubelbauer/ps-inno).

```powershell
If (!(Test-Path ntlite.exe)) {
  If (!(Test-Path ntlite-installer.exe)) {
    Write-Output "Downloading the NTLite installer"
    Invoke-WebRequest -Uri http://downloads.ntlite.com/files/NTLite_setup_x64.exe -OutFile ntlite-installer.exe  
  }

  If (!(Test-Path inno.exe)) {
    Write-Output "Downloading innoextract"
    & .\inno.ps1
  }

  Write-Output "Extracting the NTLite installer"
  # Call with the .exe to beat the default precedence of .ps1
  .\inno.exe ntlite-installer.exe
  Remove-Item ntlite-installer.exe
  Remove-Item inno.exe
  Move-Item app/NTLite.exe ntlite.exe
  Remove-Item app -Recurse
}
```

## Usage

```powershell
& .\ntlite.ps1
```
