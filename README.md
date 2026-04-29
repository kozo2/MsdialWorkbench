# MSDIAL 5 headless (command-line) version.

This repository contains only the MSDIAL 5 console/backend projects after the WPF GUI projects have been removed.
Projects such as MSDIAL 4 and MSFINDER have also been removed from this repository.

## RawDataHandler package source

The console build uses the vendor-unsupported RawDataHandler package:

`RawDataHandler-Vendor-UnSupported.1.2.9082.378.nupkg`

The package is expected in the repository-level `Assemblies` directory. `NuGet.Config` in this folder adds that local package source and `nuget.org`:

```xml
<packageSources>
  <clear />
  <add key="MS-DIAL Assemblies" value="Assemblies" />
  <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
</packageSources>
```

## Installing .NET required for build or execution

[Install .NET SDK or .NET Runtime on Ubuntu or macOS](https://dotnet.microsoft.com/download/dotnet/8.0)

## Ubuntu Linux build check

Run the following command from the root directory of this repository.

```bash
dotnet publish tests/MSDIAL5/MsdialCoreTestApp/MsdialCoreTestApp.csproj \
  --configuration "Debug vendor unsupported" \
  --framework net8 \
  --runtime linux-x64 \
  --self-contained false \
  -p:RestoreConfigFile=NuGet.Config
```

The verified publish completed with `0 Error(s)` and produced the Ubuntu/Linux x64 output at:

`tests\MSDIAL5\MsdialCoreTestApp\bin\Debug vendor unsupported\net8\linux-x64\publish\`

## macOS arm64 build check

Run the following command from the root directory of this repository.

```bash
dotnet publish tests/MSDIAL5/MsdialCoreTestApp/MsdialCoreTestApp.csproj \
  --configuration "Debug vendor unsupported" \
  --framework net8 \
  --runtime osx-arm64 \
  --self-contained false \
  -p:RestoreConfigFile=NuGet.Config
```

The verified publish completed with `0 Error(s)` and produced the macOS arm64 output at:

`tests\MSDIAL5\MsdialCoreTestApp\bin\Debug vendor unsupported\net8\osx-arm64\publish\`

Warnings are currently expected, including `MessagePack` vulnerability warnings, `zlib.net` compatibility warnings, nullable reference warnings, and obsolete API warnings.
