# 06: PowerShell and Automation

PowerShell is a powerful command-line shell and scripting language from Microsoft, built on the .NET Framework. It is the foundation of automation and management in modern Windows environments.

## 1. Introduction to PowerShell

-   **Cmdlets (Command-lets)**:
    -   The basic commands in PowerShell.
    -   They follow a `Verb-Noun` naming convention (e.g., `Get-Process`, `Stop-Service`).
    -   This makes them predictable and easy to learn.

-   **The Pipeline (`|`)**:
    -   The pipeline is used to pass the output of one cmdlet to the input of another.
    -   This allows you to chain commands together to perform complex tasks.
    -   **Example**: `Get-Process | Where-Object {$_.CPU -gt 100}` (Get all processes with CPU usage greater than 100 seconds).

-   **Objects, Not Text**:
    -   Unlike traditional shells that output text, PowerShell cmdlets output rich objects.
    -   This means you can access properties and methods of the output directly.
    -   You can use `Get-Member` to see the properties and methods of an object.
    -   **Example**: `Get-Process | Get-Member`.

-   **Help System**:
    -   PowerShell has a comprehensive help system.
    -   `Get-Help <Cmdlet-Name>`: Shows help for a specific cmdlet.
    -   `Get-Help <Cmdlet-Name> -Examples`: Shows examples of how to use the cmdlet.
    -   `Update-Help`: Downloads the latest help files.

## 2. PowerShell for Windows Administration

PowerShell can be used to manage nearly every aspect of a Windows Server.

-   **Managing Processes**:
    -   `Get-Process`: List all running processes.
    -   `Stop-Process -Name "notepad"`: Stop the Notepad process.

-   **Managing Services**:
    -   `Get-Service`: List all services.
    -   `Start-Service -Name "spooler"`: Start the Print Spooler service.
    -   `Stop-Service -Name "spooler"`: Stop the Print Spooler service.
    -   `Restart-Service -Name "spooler"`: Restart the Print Spooler service.

-   **Managing Active Directory**:
    -   Requires the `ActiveDirectory` module to be installed (`Install-WindowsFeature RSAT-AD-PowerShell`).
    -   `Get-ADUser -Filter *`: Get all users in the domain.
    -   `New-ADUser`: Create a new user.
    -   `Set-ADUser`: Modify an existing user.
    -   `Get-ADGroup -Filter *`: Get all groups.

## 3. PowerShell Remoting

-   **Purpose**: Allows you to run commands on remote computers. It is enabled by default on Windows Server 2012 and later.
-   **Protocol**: Uses WinRM (Windows Remote Management) over HTTP or HTTPS.
-   **Commands**:
    -   `Enter-PSSession -ComputerName <RemoteComputer>`: Starts an interactive session on a remote computer. Your prompt will change, and any commands you type will run on the remote machine.
    -   `Invoke-Command -ComputerName <RemoteComputer> -ScriptBlock { <Command> }`: Runs a single command or script block on one or more remote computers.
    -   **Example**: `Invoke-Command -ComputerName Server1, Server2 -ScriptBlock { Get-Service }` (Get all services from Server1 and Server2).

## 4. PowerShell Scripting

-   **File Extension**: PowerShell scripts have a `.ps1` file extension.
-   **Execution Policy**: To prevent malicious scripts from running, PowerShell has an execution policy.
    -   `Get-ExecutionPolicy`: View the current policy.
    -   `Set-ExecutionPolicy <Policy>`: Change the policy. Common policies are:
        -   `Restricted`: Default. No scripts can be run.
        -   `AllSigned`: Only scripts signed by a trusted publisher can be run.
        -   `RemoteSigned`: Locally created scripts can run, but scripts downloaded from the internet must be signed.
        -   `Unrestricted`: All scripts can run.

### Basic Script Structure

```powershell
# This is a comment

# Variables start with a $
$name = "World"

# Write output to the console
Write-Host "Hello, $name!"

# Simple loop
for ($i = 1; $i -le 5; $i++) {
    Write-Host "Count: $i"
}

# Functions
function Get-Greeting {
    param (
        [string]$UserName
    )
    return "Hello, $UserName"
}

# Call the function
$greeting = Get-Greeting -UserName "Alice"
Write-Host $greeting
```
