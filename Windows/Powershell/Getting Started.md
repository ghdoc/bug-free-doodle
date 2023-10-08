- Change theme  
    https://stackoverflow.com/questions/50611733/powershell-color-schemes
- $Host.UI.RawUI.BackgroundColor = ($bckgrnd = 'Black')
- $Host.UI.RawUI.ForegroundColor = 'White'
- $Host.PrivateData.ErrorForegroundColor = 'DarkRed'
- $Host.PrivateData.ErrorBackgroundColor = $bckgrnd
- $Host.PrivateData.WarningForegroundColor = 'Yellow'
- $Host.PrivateData.WarningBackgroundColor = $bckgrnd
- $Host.PrivateData.DebugForegroundColor = 'Yellow'
- $Host.PrivateData.DebugBackgroundColor = $bckgrnd
- $Host.PrivateData.VerboseForegroundColor = 'Green'
- $Host.PrivateData.VerboseBackgroundColor = $bckgrnd
- $Host.PrivateData.ProgressForegroundColor = 'Blue'
- $Host.PrivateData.ProgressBackgroundColor = $bckgrnd
- Clear-Host
- Install WSL manually - unix on windows  
    https://docs.microsoft.com/en-us/windows/wsl/install-manual