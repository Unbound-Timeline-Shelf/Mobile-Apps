# Windows client

Tracking Windows is a WinUI 3 desktop shell for the hosted interface. It uses
WebView2 and requires an HTTPS server address.

## Install

Download the self-contained `Unnamed-Tracking-Windows-win-x64.zip` from this
repository's [releases](https://github.com/Unbound-Timeline-Shelf/Mobile-Apps/releases),
extract it, and launch `Tracking.Windows.exe`. The release workflow publishes
the ZIP; it does not currently publish a signed MSIX. Pull-request builds also
provide a self-contained Windows artifact in the CI run.

Enter the HTTPS server address on first launch. The client stores the server
configuration locally and leaves cookies and browser storage to WebView2.

## Develop and test

On Windows with the .NET 8 SDK:

```powershell
dotnet test src/windowsapp/Tracking.Windows.Tests/Tracking.Windows.Tests.csproj -c Release
dotnet build src/windowsapp/Tracking.Windows/Tracking.Windows.csproj -c Release -p:Platform=x64
dotnet publish src/windowsapp/Tracking.Windows/Tracking.Windows.csproj -c Release -r win-x64 --self-contained true -p:Platform=x64 -p:WindowsAppSDKSelfContained=true -o artifacts/windows
```

`Tracking.Core` contains the server-address contract; `Tracking.Windows` is
the WinUI/WebView2 shell. See [client applications](../../docs/CLIENTS.md) for
the Android and PWA clients.
