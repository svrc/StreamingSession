# FoveatedStreaming Windows Sample

A Windows sample app for streaming desktop OpenXR applications to Apple Vision Pro with the Foveated Streaming framework.

This application serves as the streaming host, implementing a TCP-based session management protocol that handles device discovery, authentication, session life cycle management, and CloudXR interoperation.

## Project Structure

```
StreamingSession-WindowsApp/
├── App.config                       # Application configuration
├── App.xaml                         # WPF Application definition
├── App.xaml.cs                      # Application startup logic
├── MainWindow.xaml                  # Main window UI (XAML)
├── MainWindow.xaml.cs               # Main window code-behind
├── MainViewModel.cs                 # MVVM ViewModel for UI binding
├── ConnectionManager.cs             # Orchestrates all three connection types
├── SessionManagementConnection.cs   # TCP session management protocol
├── CloudXRConnection.cs             # NVIDIA CloudXR service management
├── BonjourConnection.cs             # mDNS service discovery
├── NvCloudXR.cs                     # P/Invoke wrapper for NVIDIA APIs
├── tcpMessageClasses.cs             # Protocol message definitions
├── FoveatedStreamingSample.sln      # Visual Studio solution file
├── FoveatedStreamingSample.csproj   # Project configuration
├── packages.config                  # NuGet package dependencies
└── Properties/                      # Assembly info and project metadata
```

## CloudXR Setup

Place the CloudXR server binaries in the same folder as your executable:

```
bin/
├── Server/
│   ├── releases/6.x.x               # NVIDIA CloudXR 6.x runtime binaries                    
│   ├── CloudXrService.exe           # NVIDIA Stream Manager CloudXR service application
│   └── NvStreamManager.exe          # NVIDIA Stream Manager application
│   └── cloudxr-runtime.yaml         # NVIDIA Stream Manager CloudXR ser
├── NvStreamManagerClient.h          # NVIDIA Stream Manager API header from their SampleClient
└── NvStreamManagerClient.dll        # NVIDIA Stream Manager DLL from their SampleClient
```

NVIDIA provides these binaries separately on NGC as two separate downloads:  [CloudXR Runtime](https://catalog.ngc.nvidia.com/orgs/nvidia/resources/cloudxr-runtime) and [CloudXR Stream Manager](https://catalog.ngc.nvidia.com/orgs/nvidia/resources/cloudxr-stream-manager?version=6.0.3). 


### Important:

To avoid conflicts, ensure the CloudXR Runtime folder exists in `Server\releases\6.x.x` where the 6.x.x is modified to the version number of the runtime (e.g. `6.0.4`)

If multiple CloudXR versions are present (e.g., both `6.0.2` and `6.0.4`), the application will choose the highest version. 

## Building

1. Open `FoveatedStreamingSample.sln` in Visual Studio 2022 or newer
2. Build the solution (Ctrl+Shift+B) or click Build > Build Solution

## Running

1. Launch FoveatedStreamingSample.exe (the CloudXR runtime is configured automatically via `XR_RUNTIME_JSON`)
2. Input your client app's bundle ID in the App Bundle ID field to advertise the endpoint over mDNS

## Requirements

- Visual Studio 2022 or newer (Windows only)
- .NET Framework 4.7.2
- Windows 10 SDK (10.0.22621.0)
