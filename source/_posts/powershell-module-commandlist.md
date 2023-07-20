---
layout: post
title: "PowerShell の コマンドの出所と出所で使えるコマンド一覧"
date: 2023-07-20 00:00:00
tags: [PowerShell]
---

# コマンド

Get-Command は gcm の alias も持つので、置き換え可です。

## コマンドがどこから参照されてるのか確認

```
> Get-Command echo
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           echo -> Write-Output

> Get-Command Write-Output
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Write-Output                                       3.1.0.0    Microsoft.PowerShell.Utility
```

## 参照元はどんなコマンドが使えるのか

```
Get-Command -Module Microsoft.PowerShell.Utility
略
Cmdlet          Get-Random                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Runspace                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-RunspaceDebug                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-TraceSource                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-TypeData                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-UICulture                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Unique                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Group-Object                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Alias                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Clixml                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Csv                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-LocalizedData                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-PSSession                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-Expression                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-RestMethod                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-WebRequest                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Measure-Command                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Measure-Object                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-Event                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-Object                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-TimeSpan                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-File                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-GridView                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-Printer                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-String                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Read-Host                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Register-EngineEvent                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Register-ObjectEvent                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-Event                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-PSBreakpoint                                3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-TypeData                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-Variable                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-Object                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-String                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-Xml                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Send-MailMessage                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-Date                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-PSBreakpoint                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-TraceSource                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Show-Command                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Sort-Object                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Start-Sleep                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Tee-Object                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Trace-Command                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Unblock-File                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Unregister-Event                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-FormatData                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-List                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-TypeData                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Wait-Debugger                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Wait-Event                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Debug                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Error                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Host                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Information                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Output                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Progress                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Verbose                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Warning                                      3.1.0.0    Microsoft.PowerShell.Utility
```

# 所感

もっとはやくしりたかった
