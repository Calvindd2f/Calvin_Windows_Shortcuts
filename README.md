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

```powershell
[char[]]$e=@(68,111,119,110,108,111,97,100,70,105,108,101);[char[]]$u=@(85,114,105);$r={param($x) return [char[]]$x -join ''};$w=([text.encoding]::ASCII).GetString([Convert]::FromBase64String('V2ViQ2xpZW50'));$c=[type]('System.Net.'+$w);$i=$c::new();& ($r.Invoke($e)) $i (&($r.Invoke($u)) 'https://chocolatey.org/install.ps1') 'install.ps1'
```
