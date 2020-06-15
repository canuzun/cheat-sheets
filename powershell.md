---
layout: page
title: PowerShell Cheat Sheet
---


| Goal | Syntax/Sample |
| -- | -- |
| PS Version | $PSVersionTable.PSVersion |
| Dynamic Powershell | Invoke-Expression $Content |
| Escape Char | ` |
| Write To File | $Content \| Out-File delete-this-tmp-file.ps1 |
| No Output | \| Out-Null |
| Output to Variable and Console | \| ($output = cmd.exe /c $arg) USE Parentheses! |
| Using Where Clause | Get-Service \| Where-Object {$_.Status -eq "Stopped"} |
| . | Get-Service \| where Status -eq "Stopped" |
| . | Get-AzRoleAssignment \| where {$_.ObjectType -EQ "User" -and $_.RoleDefinitionName -notlike "*reader*"} \| FT SignInName, DisplayName, RoleDefinitionName, ObjectType |
| Search / Find | $index = ($line \|Select-String 'TestCaseRunner Summary').Matches.Index |
| Search / Find Multiple | For multiple lines loop via array? |
| String contains/like | if($osName -like '*Windows 10*') |
| Init List | $allResources = New-Object System.Collections.Generic.List[System.Object] |
| List Contains/Except | Compare-Object -ReferenceObject @("A","B","D") -DifferenceObject @("C","D") -IncludeEqual |
| Select | $MembersObjIds = $Members \| select {$_.ObjectId} |
| CMD with Args | cmd.exe /c 'C:\"Program Files"\SmartBear\ReadyAPI-2.7.0\bin\testrunner.bat -r -a -j -fC:\TC-01\Results "-RJUnit-Style HTML Report" -FXML "-EDefault environment" C:\TC-01\readyapi-project.xml'
| . | $arg = 'C:\"Program Files"\SmartBear\ReadyAPI-2.7.0\bin\testrunner.bat -r -a -j -fC:\TC-01\Results "-RJUnit-Style HTML Report" -FXML "-EDefault environment" C:\TC-01\readyapi-project.xml' <br> cmd.exe /c $arg |
| PSCredential | $securePw = ConvertTo-SecureString "p@ss" -AsPlainText -Force <br> $credentials = New-Object System.Management.Automation.PSCredential ("userN", $securePw) |
| Loop | for($i=1; $i -le 10; $i++) {<br>Write-Host "In loop $i"<br>} |
| Date Format | [$(Get-Date -Format "yyyy-MM-dd HH:mm:ss")] |
| Get Computer Name | $env:COMPUTERNAME or hostname |
| Inline If | $(if ($isPass){'Pass'} else {'Fail'}) |
| Delay Wait-For Sleep | Start-Sleep -Seconds 5 |
| -- | -- |
| -- | -- |


#### Working With PS Modules
* Get-PSRepository
* Unregister-PSRepository -Name "PSGallery"
* Register-PSRepository -Default -InstallationPolicy Trusted
* Get-Module -ListAvailable
* Get-Module -ListAvailable -Name "AzureRM.Resources"
* RUN AS ADMIN - Update-Module -Name "AzureRM.Resources" -Force (In use warning, close all PS sessions retry)
* RUN AS ADMIN - Update-Module -Name "AzureRM" -Force
Install-Module -Name AzureRM -MinimumVersion 6.13.1 -Force (Use Force even with Trusted repos)

#### Enable/Disable Debug
Valid for session?
Sample : $DebugPreference="Continue"
* Stop: Displays the debug message and stops executing. Writes an error to the console.
* Inquire: Displays the debug message and asks you whether you want to continue. Note that adding the Debug common parameter to a command--when the command is configured to generate a debugging message--changes the value of the $DebugPreference variable to Inquire. 
* Continue: Displays the debug message and continues with execution.
* SilentlyContinue: No effect. The debug message is not (Default) displayed and execution continues without interruption.

#### Start-Job
Invoke-Expression won't work??
```powershell
$scriptBlock = {
    for($i=1; $i -le 10; $i++)
    {
        $path = "C:\ProgramData\chocolatey\lib\PIT.PQM.InstallerBCK\tmp\"
        $filename = New-Guid
        $filename = "$path$filename.txt"
        $content | Out-File $filename
    }
}

Start-Job -ScriptBlock $scriptBlock
```

#### Multi Line Script
Use @ and "
```powershell
$content = @"
while($true)
{
    Write-Host "Running..."
}
"@
```

#### .ps1 File Input Parameters
Start file with param()
```powershell
param(
$vmName
)
```
### Some References
* [Select Object](https://stackoverflow.com/questions/30149311/powershell-dot-notation-vs-select-object)
* [Capture output to variable from External Source](https://stackoverflow.com/questions/8097354/how-do-i-capture-the-output-into-a-variable-from-an-external-process-in-powershe/35980675)
* [Inline If](https://stackoverflow.com/questions/25682507/powershell-inline-if-iif)