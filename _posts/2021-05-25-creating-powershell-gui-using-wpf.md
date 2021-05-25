---
layout: post
published: true
title: Creating Powershell GUI using WPF
date: '2016-01-06'
---
# Creating WPF Powershell GUI

Creating a powershell GUI is really simple but it can be hard to find the right informaiton. I started off using PoshGUI.com to create the GUI using winforms but that tool became a paid tool so that was the end of that and I had to find an alternative. Also, the experience of using PoshGUI was good but not the best. The following code provides a template but you can create your own UI using WPF app in Visual Studio.

# Step 1: Create powershell script for GUI
Create a powershell script file. Call it `helloworld.gui.ps1` (you will see what it is has a .gui post fix soon).

Add the following code snippet

```powershell
Add-Type -AssemblyName PresentationFramework

[xml]$xaml = @"
<Window
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Hello GUI" Height="609.41" Width="394.383">

        <Grid Margin="0,0,4,-8">
        <Grid.RowDefinitions>
            <RowDefinition Height="49*"/>
            <RowDefinition/>
        </Grid.RowDefinitions>
            <Label Content="Your name:" HorizontalAlignment="Left" Margin="10,10,0,0" VerticalAlignment="Top"/>
            <TextBox x:Name="txtYourName" HorizontalAlignment="Left" Height="23" Margin="130,14,0,0" Text="Bruce Willis" VerticalAlignment="Top" Width="234"/>

            <Button x:Name="btnRun" Content="Cast Away" HorizontalAlignment="Left" Margin="291,543,0,0" VerticalAlignment="Top" Width="63" />
        </Grid>
</Window>
"@

#############################
# Map Controls
#############################

$reader=(New-Object System.Xml.XmlNodeReader $xaml)
$Window=[Windows.Markup.XamlReader]::Load( $reader )

$txtYourName = $Window.FindName("txtYourName")
$btnRun = $Window.FindName("btnRun")

#############################
# Hook Events
#############################
$btnRun.Add_Click({ RunCode })

##########################
# Functions
##########################
function RunCode()
{
    $powershellScriptPath = "`"" + $PSScriptRoot + "\helloworld.ps1`""

    $name = "`"" + $txtYourName.Text + "`""
    $argList = "-file $powershellScriptPath `
                -name $name `
                "

    Start-Process powershell -argumentlist $argList
}

##########################
## Display the UI
##########################

$Window.ShowDialog() | Out-Null
```

# Step 2: Create .bat file to launch the pervious file with double click
Create a new file. Name it `helloWorld.gui.bat` (make sure that the this file name matches the previous file apart from the final extension)

```powershell
@ECHO OFF
PowerShell.exe -NoProfile -Command "& {Start-Process PowerShell.exe -ArgumentList '-NoProfile -WindowStyle Hidden -ExecutionPolicy Bypass -File ""%~dpn0.ps1""' -Verb RunAs}"
```

# Step 3: Create a new powershell file which the gui will call to execute code
This is optional but sometimes you want the GUI to just collect information and call another powershell to do some powerfull stuff. Name this file `helloworld.ps1` and add the following code

```powershell
param ( $name )

Write-Host "Hello $name"

PAUSE
```

# Step 4: Celebrate
This is just a template code and the possibilities are endless. You dont have to create step 3. You could just execute all the logic in the gui.ps1 file but sometimes you may want to just execute poweshell script to do the final leg work and let the user see/handle the errors.
