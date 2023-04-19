# Calvin_Windows_Shortcuts
Windows shortcuts and one liners


## Install Chocolately package manager as pwsh1liner
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```


## Install Chocolatey again
```powershell
$u='https://chocolatey.org/install.ps1';$o='install.ps1';$w=([text.encoding]::ASCII).GetString([Convert]::FromBase64String('V2ViQ2xpZW50'));$m=([text.encoding]::ASCII).GetString([Convert]::FromBase64String('RG93bmxvYWRGaWxl'));$c=[type]('System.Net.'+$w);$i=$c::new();$i.$m.Invoke($i, ($u, $o))
```


## This script uses the following obfuscation techniques:

Encode the method and property names as arrays of character codes.  
Use script blocks and invoke them with the call operator (&).  
Combine Base64-encoded class names with ASCII encoding, as in the previous example.  
  
```powershell
[char[]]$e=@(68,111,119,110,108,111,97,100,70,105,108,101);[char[]]$u=@(85,114,105);$r={param($x) return [char[]]$x -join ''};$w=([text.encoding]::ASCII).GetString([Convert]::FromBase64String('V2ViQ2xpZW50'));$c=[type]('System.Net.'+$w);$i=$c::new();& ($r.Invoke($e)) $i (&($r.Invoke($u)) 'https://chocolatey.org/install.ps1') 'install.ps1'
```


### Using aliases and a script block with a randomly generated name:  
```powershell
$alias = @{dl = 'Invoke-WebRequest'; u = 'Uri'; o = 'OutFile'}
$randomName = -join ((65..90) + (97..122) | Get-Random -Count 8 | % {[char]$_})
${function:$randomName} = {
    param($url, $file)
    & $alias.dl -Uri $url -OutFile $file
}
& $randomName 'https://chocolatey.org/install.ps1' 'install.ps1'
```

### Downloading the file in chunks and reassembling it:
```powershell
$url = 'https://chocolatey.org/install.ps1'
$outputFile = 'install.ps1'
$webClient = New-Object System.Net.WebClient
$response = $webClient.GetResponse()
$totalSize = [long]$response.ContentLength
$response.Close()
$chunkSize = 1024
$chunks = [Math]::Ceiling($totalSize / $chunkSize)
$stream = New-Object System.IO.FileStream($outputFile, [System.IO.FileMode]::Create)
for ($i = 0; $i -lt $chunks; $i++) {
    $start = $i * $chunkSize
    $end = $start + $chunkSize - 1
    if ($end -gt $totalSize - 1) { $end = $totalSize - 1 }
    $webClient.Headers['Range'] = "bytes=$start-$end"
    $buffer = $webClient.DownloadData($url)
    $stream.Write($buffer, 0, $buffer.Length)
}
$stream.Close()
```

### CSharp stufff
```powershell
$sourceCode = @"
using System;
using System.IO;
using System.Net;

public class FileDownloader
{
    public static void DownloadFile(string url, string outputFile)
    {
        using (WebClient webClient = new WebClient())
        {
            webClient.DownloadFile(url, outputFile);
        }
    }
}
"@

Add-Type -TypeDefinition $sourceCode -Language CSharp

$url = 'https://chocolatey.org/install.ps1'
$outputFile = 'install.ps1'
[FileDownloader]::DownloadFile($url, $outputFile)
```

### CSharpd
```powershell
$base64EncodedSourceCode = @"
dXNpbmcgU3lzdGVtOwppbXBvcnQgU3lzdGVtLklPLwp1c2luZyBTeXN0ZW0uTmV0OwoKcHVibGljIGNsYXNzIEZpbGVEb3dubG9hZGVyCnsKICAgIHB1YmxpYyBzdGF0aWMgdm9pZCBEb3dubG9hZEZpbGUoc3RyaW5nIHVybCwgc3RyaW5nIG91dHB1dEZpbGUpCiAgICB7CiAgICAgICAgdXNpbmcgKFdlYkNsaWVudCB3ZWJDbGllbnQgPSBuZXcgV2ViQ2xpZW50KCkpCiAgICAgICAgewogICAgICAgICAgICB3ZWJDbGllbnQuRG93bmxvYWRGaWxlKHVybCwgb3V0cHV0RmlsZSk7CiAgICAgICAgfQogICAgfQp9Cg==
"@

$sourceCode = [Text.Encoding]::ASCII.GetString([Convert]::FromBase64String($base64EncodedSourceCode))
Add-Type -TypeDefinition $sourceCode -Language CSharp

$url = 'https://chocolatey.org/install.ps1'
$outputFile = 'install.ps1'
[FileDownloader]::DownloadFile($url, $outputFile)

```
