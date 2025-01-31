---
title: Azure N-series AMD GPU driver setup for Windows
description: How to set up AMD GPU drivers for N-series VMs running Windows Server or Windows in Azure
author: vikancha-MSFT
manager: jkabat
ms.service: azure-virtual-machines
ms.subservice: sizes
ms.collection: windows
ms.topic: how-to
ms.date: 04/13/2023
ms.author: vikancha
---

# Install AMD GPU drivers on N-series VMs running Windows

**Applies to:** Windows VMs :heavy_check_mark: Flexible scale sets 

## NGads V620 Series ##
The AMD Software: Cloud Edition drivers must be installed to take advantage of the GPU capabilities of Azure NGads V620 Series VMs.

### Requirements

| OS | Driver |
| -------- |------------- |
| Windows 11 64-bit version 21H2, 22H2<br/><br/>Windows 10 64-bit version 21H2, 22H2 <br/><br/>Windows 11 EMS 64-bit 21H2, 22H2<br/><br/> Windows 10 EMS 64-bit 21H2, 22H2<br/><br/>Windows Server 2019 LTSC (version 1809)<br/><br/>Windows Server 2022 64-bit Release 20348 | [23.Q3 (.exe)](https://go.microsoft.com/fwlink/?linkid=2248541) |

### VM Creation
Create the VMs using CLI. (Azure AMD GPU driver extensions don't support NGads  V620 Series during preview)
1. Review the [CLI VM creation documentation](/azure/virtual-machines/windows/quick-create-cli).

### Driver installation
1.	Connect by Remote Desktop to each NGads V620-series VM<br>
2. Download the EXE file to a local drive<br>
3. If you need to uninstall the previous driver version, run "setup.exe -factoryresetinstall" from a command line <br>
4.	For a first-time driver installation, double-click or run “setup.exe” from a command line<br>
5. Reboot the VM

### Verify driver installation
1.	You can verify driver installation in Device Manager. The following example shows successful configuration of the Radeon Pro V620 card on an Azure NGads V620 VM. The exact driver date and version will depend on the driver package released.


## NVv4 Series ##
To take advantage of the GPU capabilities of the new Azure NVv4 series VMs running Windows, AMD GPU drivers must be installed. The [AMD GPU Driver Extension](../extensions/hpccompute-amd-gpu-windows.md) installs AMD GPU drivers on a NVv4-series VM. Install or manage the extension using the Azure portal or tools such as Azure PowerShell or Azure Resource Manager templates. See the [AMD GPU Driver Extension documentation](../extensions/hpccompute-amd-gpu-windows.md) for supported operating systems and deployment steps.

If you choose to install AMD GPU drivers manually, this article provides supported operating systems, drivers, and installation and verification steps.

Only GPU drivers published by Microsoft are supported on NVv4 VMs. Don't install GPU drivers from any other source.

For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](../sizes-gpu.md?toc=/azure/virtual-machines/windows/toc.json).



### Supported operating systems and drivers

| OS | Driver |
| -------- |------------- |
| Windows 11 64-bit 21H2, 22H2, 23H2<br/><br/>Windows 10 64-bit 21H2, 22H2, 20H2 <br/><br/> | [23.Q3](https://download.microsoft.com/download/0/8/1/081db0c3-d2c0-44ae-be45-90a63610b16e/AMD-Azure-NVv4-Driver-23Q3-win10-win11.exe) (.exe) |
| Windows Server 2022, Windows 11 EMS <br/><br/> | [23.Q3](https://download.microsoft.com/download/2/d/3/2d328d15-4188-4fdb-8912-fb300a212dfc/AMD-Azure-NVv4-Driver-23Q3-winsvr2022.exe) (.exe)
| Windows Server 2019, Windows 10 EMS <br/><br/> | [23.Q3](https://download.microsoft.com/download/e/8/8/e88bb244-b8e8-47cc-9f86-9ba2632b3cb6/AMD-Azure-NVv4-Driver-23Q3-winsvr2019.exe) (.exe)

Previous supported driver versions for Windows builds up to 1909 are [20.Q4-1](https://download.microsoft.com/download/0/e/6/0e611412-093f-40b8-8bf9-794a1623b2be/AMD-Azure-NVv4-Driver-20Q4-1.exe) (.exe) and [21.Q2-1](https://download.microsoft.com/download/4/e/a/4ea28d3f-28e2-4eaa-8ef2-4f7d32882a0b/AMD-Azure-NVv4-Driver-21Q2-1.exe) (.exe) 
 
 > [!NOTE]
   >  If you use build 1903/1909 then you may need to update the following group policy for optimal performance. These changes are not needed for any other Windows builds.
   >  
   >  [Computer Configuration->Policies->Windows Settings->Administrative Templates->Windows Components->Remote Desktop Services->Remote Desktop Session Host->Remote Session    Environment], set the Policy [Use WDDM graphics display driver for Remote Desktop Connections] to Disabled.
   >  

## NVadsV710_v5 Series (In Preview) ##
During the preview program manually download and install the following Windows drivers. Azure GPU driver extension will support the NVadsV710_v5 Series at GA.

| OS | Driver |
| -------- |------------- |
| Windows 10, Windows 11 64-bit 21H2, 22H2, 23H2<br/><br/>Windows 10 64-bit 21H2, 22H2, 20H2 <br/><br/> | [24.Q3](https://go.microsoft.com/fwlink/?linkid=2291063) (.exe) |
| Windows Server 2022, Windows 11 EMS <br/><br/> | [24.Q3](https://go.microsoft.com/fwlink/?linkid=2292204) (.exe)
| Windows Server 2019, Windows 10 EMS <br/><br/> | [24.Q3](https://go.microsoft.com/fwlink/?linkid=2292402) (.exe)
 
### Driver installation
> [!NOTE]
   >  Follow these steps if you see "Error 184 - AMD Installer cannot cpontinue due to an unsupported Operating System" error on Windows 10 EMS / Windows 11 EMS.
   >  
   >  Go to C:\AMD\AMD Software Azure NVv4 Guest Driver 23Q3\Packages\Drivers\Display\WT6A_INF
   >  Right click and  install on the *.inf file.
  > 
  >   For Windows10 EMS: u9397288.inf
  > 
  >   For Windows11 EMS: u2397344.inf 

1. Connect by Remote Desktop to each NVv4-series VM.

2. If you need to uninstall the previous driver version, download the [AMD cleanup utility](https://download.microsoft.com/download/4/f/1/4f19b714-9304-410f-9c64-826404e07857/AMDCleanupUtilityni.exe). Don't use the utility that comes with the previous version of the driver.

3. Download and install the latest driver.

4. Reboot the VM.

### Verify driver installation

1. You can verify driver installation in Device Manager. The following example shows successful configuration of the Radeon Instinct MI25 card on an Azure NVv4 VM.
<br />

![Screenshot that shows successful configuration of the Radeon Instinct MI25 card on an Azure NVv4 VM.](./media/n-series-amd-driver-setup/device-manager.png)

2. You can use dxdiag to verify the GPU display properties including the video RAM. The following example shows a 1/2 partition of the Radeon Instinct MI25 card on an Azure NVv4 VM.
<br />
![Screenshot that shows a 1/2 partition of the Radeon Instinct MI25 card on an Azure NVv4 VM.](./media/n-series-amd-driver-setup/dxdiag-output-new.png)

3. If you're running Windows 10 build 1903 or higher, dxdiag shows no information in the 'Display' tab. Use the 'Save All Information' option at the bottom and the output file shows the information related to AMD MI25 GPU.

![GPU driver properties](./media/n-series-amd-driver-setup/dxdiag-details.png)
