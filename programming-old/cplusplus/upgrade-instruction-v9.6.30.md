---
layout: default-layout
title: Upgrade Instruction - Dynamsoft Barcode Reader SDK C++ Edition
description: This page shows how to upgrade to version 9.x.
keywords: Upgrade, how-to guides
needAutoGenerateSidebar: false
permalink: /programming/cplusplus/upgrade-instruction-v9.6.30.html
---


# How to Upgrade to Version 9.x  

## From version 8.x

- You need to replace the old assembly files with the ones in the latest version. Download the latest version [here](https://www.dynamsoft.com/Downloads/Dynamic-Barcode-Reader-Download.aspx).

- Go to <a href="https://www.dynamsoft.com/customer/license/fullLicense" target="_blank">Customer Portal</a> to get your license key.

- Update your code to set the license
```cpp
  char errorBuf[512];
  dynamsoft::dbr::CBarcodeReader::InitLicense("YOUR-LICENSE-KEY", errorBuf, 512);
  CBarcodeReader* reader = CBarcodeReader::GetInstance();
  if(reader != NULL)
  {
      // Add your code here to call decoding method, process barcode results and so on
      // ...
      reader->Recycle();
  }
```

>Note:
>The following license activation related functions have been deprecated, they still work in this version but could be removed in version 10.0. We recommend you to use InitLicense to set the license.

- `InitLicenseFromDLS`
- `InitLicenseFromServer`
- `InitLicenseFromLicenseContent` 

## From version 7.x

- You need to replace the old assembly files with the ones in the latest version. Download the latest version [here](https://www.dynamsoft.com/Downloads/Dynamic-Barcode-Reader-Download.aspx).

- Go to <a href="https://www.dynamsoft.com/customer/license/fullLicense" target="_blank">Customer Portal</a> to get your license key.

- Update your code to set the license
```cpp
  char errorBuf[512];
  dynamsoft::dbr::CBarcodeReader::InitLicense("YOUR-LICENSE-KEY", errorBuf, 512);
  CBarcodeReader* reader = CBarcodeReader::GetInstance();
  if(reader != NULL)
  {
      // Add your code here to call decoding method, process barcode results and so on
      // ...
      reader->Recycle();
  }
```

>Note:
>The following license activation related functions have been deprecated, they still work in this version but could be removed in version 10.0. We recommend you to use InitLicense to set the license.

- `InitLicenseFromServer`
- `InitLicenseFromLicenseContent` 


## From version 6.x

We made some structural updates in the new version. To upgrade from 6.x to 9.x, we recommend you to review our sample code and re-write the barcode scanning module.
