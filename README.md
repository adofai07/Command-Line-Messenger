# Command Line Messenger

This project aims for making a working messenger in your terminal.

## Fetching messages (and history)

This messenger uses `git` requests to upload/download messages.

### *Uploading messages*

Python:

```py
with open("path-to-repo/Messages001.txt", "a") as f:
    f.write("Hello")
```

Powershell:

```powershell
cd "path-to-repo"
git add .
git commit -m "2023 Nov. 17 21:05:29"
git push -u origin main
```

## Sending notifications

This messenger uses balloon tips to send notifications. (Powershell required)

```powershell
function ShowBalloonTipInfo {    
    [CmdletBinding()]
    param (
        [string]$Title,
        [string]$Text,
        # It must be 'None', 'Info', 'Warning', 'Error'
        [string]$Icon = 'Info'
    )
    
    Add-Type -AssemblyName System.Windows.Forms
    
    if ($null -eq $script:balloonToolTip) {
        $script:balloonToolTip = New-Object System.Windows.Forms.NotifyIcon 
    }
    
    $path = Get-Process -id $pid | Select-Object -ExpandProperty Path
    $balloonToolTip.Icon = [System.Drawing.Icon]::ExtractAssociatedIcon($path)
    $balloonToolTip.BalloonTipIcon = $Icon
    $balloonToolTip.BalloonTipText = $Text
    $balloonToolTip.BalloonTipTitle = $Title
    $balloonToolTip.Visible = $true

    $balloonToolTip.ShowBalloonTip(3000)
}
```

For example, if a person named `adofai` sent 3 messages, the function would be called like:

```powershell
ShowBalloonTipInfo -Title "adofai" -Text "3 messages"
```
