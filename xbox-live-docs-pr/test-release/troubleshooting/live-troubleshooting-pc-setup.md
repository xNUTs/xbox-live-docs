---
title: Troubleshooting Xbox Live setup on Windows 10 PC
description: Ensuring that your Windows 10 PC is set up as an Xbox Live development environment.
ms.assetid: 9cfebdcd-0c1c-4fc2-9457-e7e434b6374c
ms.date: 04/04/2017
ms.topic: article
keywords: xbox live, xbox, games, uwp, windows 10, xbox one, troubleshoot
ms.localizationpriority: medium
---

# Troubleshooting Xbox Live setup on Windows 10 PC

On Windows 10 PC, ensure that your machine is set up correctly, as follows:

1. Change your machine to point to the XDKS.1 sandbox where samples are designed to run.
   Do this by running this script:

```cmd
{*SDK source root*}\Tools\SwitchSandbox.cmd XDKS.1
```

1. Extract the contents of the zip file "SourcesAndSamples.zip" found inside the SDK.

1. Open a sample solution:

    * For C++ API: {*SDK source root*}\Samples\Social\UWP\Cpp\Social.Cpp.140.sln

    * For WinRT API with C#: {*SDK source root*}\Samples\Social\UWP\CSharp\Social.CSharp.140.sln

    * For WinRT API with C++/CX:  {*SDK source root*}\Samples\TitleStorage\UWP\CppCx\TitleStorageUniversal.sln

1. Change the build target platform to "x64".

1. Right-click the solution and re-build everything.

1. Launch the app in the debugger.

1. Sign-in with a retail developer account or test account.
   The account must be authorized in [Partner Center](https://partner.microsoft.com/dashboard).

1. Grant the app permission to access your Xbox Live information.

1. Verify that the app can retrieve your information and you can see your gamertag.
