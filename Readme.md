# Unofficial SimpleITK Cross-Platform Runtime for .NET 8

[![NuGet Version](https://img.shields.io/nuget/v/SachaBr.SimpleITK.Runtime.svg)](https://www.nuget.org/packages/SachaBr.SimpleITK.Runtime/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This repository contains an **unofficial** NuGet packaging of the [SimpleITK](https://github.com/SimpleITK/SimpleITK) C# binaries, structured and optimized for modern **.NET 8+** cross-platform applications (Windows x64 and Linux x64).

## Project Structure

To maintain a clear separation between the packaging configuration and the original upstream files, the repository is organized using a vendoring approach:

* **`/SachaBr.SimpleITK.Runtime.csproj`** — The master .NET project file used to build the NuGet package.
* **`/3dparty/SimpleITK/`** — Isolated directory containing unmodified original assets from the SimpleITK project (`LICENSE`, `NOTICE`, `Readme.md`, `.dll`, and `.so` files).

## Package Identity & Status

* **Package ID:** `SachaBr.SimpleITK.Runtime`
* **Target Framework:** `.NET 8.0`
* **Supported RIDs:** `win-x64`, `linux-x64`
* **Modifications:** The original binary files (`SimpleITKCSharpManaged.dll`, `SimpleITKCSharpNative.dll`, and `libSimpleITKCSharpNative.so`) **have not been modified** or recompiled.
* **Structure Changes:** The files were rearranged into standard NuGet layout (`runtimes/` and `lib/`) during the packing process to leverage automatic native library deployment (Runtime IDentifier) in modern .NET execution environments.

## Installation

Install the package via .NET CLI:

```bash
dotnet add package SachaBr.SimpleITK.Runtime --version 2.3.1.1
```

## Quick Start

You can verify that both the managed wrapper and the underlying native companion (`.dll` on Windows / `.so` on Linux) are loaded correctly by calling the `ExtendedVersionString()` method, which outputs comprehensive versioning data for both SimpleITK and the underlying ITK core:

```csharp
using System;
using itk.simple;

class Program
{
    static void Main()
    {
        try
        {
            // Interrogates the native library layer to verify successful P/Invoke binding
            Console.WriteLine("--- SimpleITK Environment Info ---");
            Console.WriteLine(Version.ExtendedVersionString());
            Console.WriteLine("----------------------------------");
            Console.WriteLine("Package is successfully attached and operational!");
        }
        catch (DllNotFoundException ex)
        {
            Console.WriteLine("Error: Failed to load the native SimpleITK binary component.");
            Console.WriteLine(ex.Message);
        }
    }
}
```

## License & Copyright

The SimpleITK software is distributed under the **Apache License 2.0**. 
The copyright is held by **NumFOCUS** and the **Insight Software Consortium**.

* This package is distributed **"AS IS", without warranties of any kind**, either express or implied.
* Original `LICENSE` and `NOTICE` documents are strictly preserved and bundled inside the **`3dparty/SimpleITK/`** directory of the resulting NuGet package.
* This is a community repackaging effort and is **not** an official release or endorsed by the SimpleITK Team.
