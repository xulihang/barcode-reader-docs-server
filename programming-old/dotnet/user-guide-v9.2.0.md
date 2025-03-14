---
layout: default-layout
title: User Guide - Dynamsoft Barcode Reader SDK .NET Edition
description: This is the user guide of Dynamsoft Barcode Reader SDK .NET Edition.
keywords: user guide, .Net
needAutoGenerateSidebar: true
needGenerateH3Content: true
noTitleIndex: true
permalink: /programming/dotnet/user-guide-v9.2.0.html
---

# Getting Started with .Net
In this guide, you will learn step by step on how to build a barcode reading application with Dynamsoft Barcode Reader SDK using .Net.

## Requirements

- Operating Systems:
    - Windows 7, 8, 10, 11
    - Windows Server 2003, 2008, 2008 R2, 2012, 2016, 2019, 2022

- Developing Environment:
   - Visual Studio 2008 or above
   - .NET Framework 2.0, .NET Framework 4.0 or above
   - .NET Core 3.1
   - .NET 5.0 or 6.0

>Note:
>Dynamsoft Barcode Reader provides both online and offline license options. The online license option might not work in an environment that doesn't have network connection or some environments like AWS Lambda. In such case, you can get an offline trial license key via <a href="https://www.dynamsoft.com/customer/license/trialLicense?utm_source=guide&product=dbr&package=desktop" target="_blank">Customer Portal</a> or by <a href="https://www.dynamsoft.com/company/contact/" target="_blank">contacting us</a>.

<iframe width="400" height="225" src="https://www.youtube.com/embed/QjrP9EC6IlA" title="How to Use Dynamsoft Barcode Reader .NET SDK | Dynamsoft Tutorial" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Installation
If you haven't downloaded the SDK yet, download the `.NET Package` now from <a href="https://www.dynamsoft.com/barcode-reader/downloads/?utm_source=docs" target="_blank">Dynamsoft website</a> and unzip the package into the directory of your choice. After you unzip the file, you can find samples for supported platforms in the **Samples** folder under the installation folder.

>For this tutorial, the folder we unzip the SDK to will be referred to as `[INSTALLATION FOLDER]`, so please be aware of that as you go through the rest of this guide.

> You can also download the [Dynamsoft.DotNet.Barcode nuget Package](https://www.nuget.org/packages/Dynamsoft.DotNet.Barcode/) which supports .NET Framework 2.0/4.0, .NET Core 3.1, .NET 5.0/6.0.

## Build Your First Application
Let's start by creating a console application which demonstrates how to use the minimum code to read barcodes from an image file.  
>You can download the entire source code and compiled program [here](https://download2.dynamsoft.com/samples/dbr/user-guide/dbr-csharp-sample.zip).

### Create a New Project 

1. Start Visual Studio and create a new Console Application in C#. Let's name it `DBRCSharpSample`.

### Add the Library Reference
1. Follow one of the below steps to add Dynamsoft Barcode Reader SDK to your project.
   - Right click on Project -> Add -> Reference, Browse to `[INSTALLATION FOLDER]\Lib\4.0` and Select `Dynamsoft.BarcodeReader.dll` and `DynamsoftCommon.dll`.
   >Browse to `[INSTALLATION FOLDER]\Lib\2.0` if you want to use .NET Framework 2.0.
   - Right click on Project -> Manage NuGet Packages, Search and Install package `Dynamsoft.DotNet.Barcode`.
   - If you are developing using .NET Core, click on Project -> Manage NuGet Packages, Search and Install package `Dynamsoft.NetCoreApp.Barcode`.

2. Add the namespace in `Program.cs`.
   ```csharp
    using Dynamsoft;
    using Dynamsoft.DBR;
   ```

### Initialize a Barcode Reader Instance
1. Create an instance of Dynamsoft Barcode Reader.

    ```csharp
    string errorMsg;
    BarcodeReader.InitLicense("<insert DBR license key here>", out errorMsg);
    BarcodeReader reader = new BarcodeReader();
    ```
    
    >Please replace `<insert DBR license key here>` with a valid DBR licensekey. There are two ways to obtain one:
    >- Search `DBRLicense` and find the license from `[INSTALLATION FOLDER]\Samples\BarcodeReaderDemo\BarcodeReaderDemo\App.config`.
    >- Request a trial license from <a href="https://www.dynamsoft.com/customer/license/trialLicense?utm_source=guide&product=dbr&package=desktop" target="_blank">Customer Portal</a>. 

### Configure the Barcode Scanning Behavior
1. Set barcode format and count to read.

    ```csharp
    PublicRuntimeSettings runtimeSettings = reader.GetRuntimeSettings();
    runtimeSettings.BarcodeFormatIds = (int)EnumBarcodeFormat.BF_ALL;
    runtimeSettings.BarcodeFormatIds_2 = (int)(EnumBarcodeFormat_2.BF2_POSTALCODE | EnumBarcodeFormat_2.BF2_DOTCODE);
    runtimeSettings.ExpectedBarcodesCount = 32;
    reader.UpdateRuntimeSettings(runtimeSettings);
    ```

    >The barcode formats to enable is highly application-specific. We recommend that you only enable the barcode formats your application requires. Check out [Barcode Format Enumeration]({{ site.dotnet_enumerations }}format-enums.html) for full supported barcode formats. 

    >If you know exactly the barcode count you want to read, specify `ExpectedBarcodesCount` to speed up the process and improve the accuracy. 

### Decode and Output Results 
1. Decode barcodes from an image file.
2. Get and output barcode results.

    ```csharp
    TextResult[] results;
    try
    {
        results = reader.DecodeFile(@"[INSTALLATION FOLDER]/Images/AllSupportedBarcodeTypes.png", "");
        Console.WriteLine("Total barcodes found: " + results.Length);
        for (int iIndex = 0; iIndex < results.Length; ++iIndex)
        {
            Console.WriteLine("Barcode " + (iIndex + 1));
            if (results[iIndex].BarcodeFormat != 0)
            {
                Console.WriteLine("    Barcode Format: " + results[iIndex].BarcodeFormatString);
            }
            else
            {
                Console.WriteLine("    Barcode Format: " + results[iIndex].BarcodeFormatString_2);
            }
            Console.WriteLine("    Barcode Text: " + results[iIndex].BarcodeText);
        }
 
    }
    catch (BarcodeReaderException exp)
    {
        Console.WriteLine(exp.Message);
    }
    ```

    >For the error handling mechanism, the SDK throws [BarcodeReaderException]({{site.dotnet_class}}BarcodeReaderException.html) for each function. You should add codes for exception handling based on your needs. 

    >The SDK returns multiple barcode information, including barcode count, barcode format, barcode text, location, barcode raw data, etc. Check out [TextResult]({{ site.dotnet_class }}TextResult.html) for full supported result data.

### Release Resource

1. Destroy the instance to release all resources.

    ```csharp
    reader.Dispose();
    ```

>Note:  
Please change all `[INSTALLATION FOLDER]` in above code snippet to your unpacking path.


### Build and Run the Project

1. In Visual Studio, build the project to generate program `DBRCSharpSample.exe`.

2. Run the program `DBRCSharpSample.exe`.

 >If you got the exception "Failed to create compression directory" or "Failed to load module dll", please copy `x64` and `x86` folders to the folder where `Dynamsoft.BarcodeReader.dll` and `DynamsoftCommon.dll` resides and try again. The `x64` and `x86` folders can be found under `[INSTALLATION FOLDER]\Lib\2.0` or `[INSTALLATION FOLDER]\Lib\4.0`.


>You can download the entire source code and compiled program from [Here](https://download2.dynamsoft.com/samples/dbr/user-guide/dbr-csharp-sample.zip).

## Next Steps

- Learn [How to Upgrade to Latest Version]({{site.dotnet}}upgrade-instruction.html)
- [Explore SDK Features]({{site.dotnet}}user-guide/explore-features/index.html)
- See how the SDK works in [Popular Use Cases]({{site.dotnet}}user-guide/use-cases/index.html)
- Check out the [Official Samples and Demo]({{site.dotnet}}samples/index.html)

