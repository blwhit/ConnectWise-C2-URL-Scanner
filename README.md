# ConnectWise-C2-URL-Scanner

A command-line PowerShell tool to extract suspicious relay URLs hidden in ConnectWise ScreenConnect executables.  
It scans raw strings from the binary hunting for potential command-and-control (C2) URLs that may be embedded using certificate stuffing techniques.

---

## Behavior

- By default, the script looks for known keywords (e.g., `relay`, `screenconnect`, `instance`, etc.) and screens for `.screenconnect.com` URLs.
- You can override the keyword list entirely using the `-Strings` parameter to search for **custom patterns**.

---

## Usage

### Step 1 – Set your target executable path

```powershell
$filepath = "C:\Path\To\ConnectWise.exe"
```


### Step 2 – Run the script remotely as a temp file

#### One Liner

```powershell
$u="$env:TEMP\ConnectWise-C2-URL-Scanner.ps1"; iwr -UseBasicParsing "https://raw.githubusercontent.com/blwhit/ConnectWise-C2-URL-Scanner/main/ConnectWise-C2-URL-Scanner.ps1" -OutFile $u; powershell -ExecutionPolicy Bypass -File $u -FilePath $filepath; rm $u -Force

```
#### Script

```powershell
$ConnectWiseC2URLScanner = "$env:TEMP\ConnectWise-C2-URL-Scanner.ps1"

Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/blwhit/ConnectWise-C2-URL-Scanner/main/ConnectWise-C2-URL-Scanner.ps1" -OutFile $ConnectWiseC2URLScanner

powershell -ExecutionPolicy Bypass -File $ConnectWiseC2URLScanner -FilePath $filepath

Remove-Item $ConnectWiseC2URLScanner -Force
```

---

## Parameters

| Parameter   | Type       | Description                                                                     |
| ----------- | ---------- | --------------------------------------------------------------------------------|
| `-FilePath` | `String`   | **(Required)** Path to the `.exe` file to analyze.                              |
| `-Strings`  | `String[]` | *(Optional)* Define suspicious keywords to hunt with your own array of strings. |

---

### Example: Custom String Match

```powershell
.\ConnectWise-C2-URL-Scanner.ps1 -FilePath "C:\ConnectWise.exe" -Strings @("screenconnect", "instance", "relay")
```

---
