# MS-DIAL 5 Console Build Check

This subtree contains the MS-DIAL 5 console/backend projects after removing the WPF GUI projects.

## RawDataHandler package source

The console build uses the vendor-unsupported RawDataHandler package:

`RawDataHandler-Vendor-UnSupported.1.2.9082.378.nupkg`

The package is expected in the repository-level `Assemblies` directory. `NuGet.Config` in this folder adds that local package source and `nuget.org`:

```xml
<packageSources>
  <clear />
  <add key="MS-DIAL Assemblies" value="..\..\Assemblies" />
  <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
</packageSources>
```

## Build check

Run the build check from `src/MSDIAL5`:

```powershell
$env:DOTNET_CLI_HOME = (Resolve-Path .).Path
$env:DOTNET_SKIP_FIRST_TIME_EXPERIENCE = '1'
$env:DOTNET_CLI_TELEMETRY_OPTOUT = '1'

dotnet build ..\..\tests\MSDIAL5\MsdialCoreTestApp\MsdialCoreTestApp.csproj `
  --configuration "Debug vendor unsupported" `
  --framework net8 `
  -p:RestoreConfigFile=NuGet.Config
```

The verified build completed with `0 Error(s)` and produced the console executable at:

`tests\MSDIAL5\MsdialCoreTestApp\bin\Debug vendor unsupported\net8\MSDIALCUI.exe`

Warnings are currently expected, including `MessagePack` vulnerability warnings, `zlib.net` compatibility warnings, nullable reference warnings, and obsolete API warnings.
