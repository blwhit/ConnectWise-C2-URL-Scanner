# ConnectWise-C2-URL-Scanner

A command-line PowerShell tool to extract relay URLs hidden in ConnectWise ScreenConnect executables.  
It scans Authenticode certificate fields to find command-and-control (C2) URLs often stuffed by attackers.

---

## Usage

Set file path
```
$filepath = "C:\YourFilePath.exe"
```
Download and run script remotely as tempfile
```
$ConnectWiseC2URLScanner = "$env:TEMP\ConnectWise-C2-URL-Scanner.ps1"; Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/blwhit/ConnectWise-C2-URL-Scanner/refs/heads/main/ConnectWise-C2-URL-Scanner.ps1" -OutFile $ConnectWiseC2URLScanner; powershell -ExecutionPolicy Bypass -File $ConnectWiseC2URLScanner -FilePath $filepath; Remove-Item $ConnectWiseC2URLScanner -Force
```
