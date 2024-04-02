<img align="right" src="https://github.com/n00b69/SAMSUNG-WINNER-WindowsARM/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Installation

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)
  
- [Drivers](https://github.com/n00b69/woa-winner/releases/tag/Drivers)

- [Modded TWRP](https://github.com/n00b69/woa-winner/releases/tag/Recovery) (should already be installed)


### Reboot to TWRP
> Disable MTP in TWRP

#### Entering mass storage mode
```cmd
adb shell msc.sh
```

### Correct disk mapping in Windows disk manager 
https://sourceforge.net/projects/gptfdisk/files/gptfdisk/
https://mega.nz/file/K5UkQLrC#vCwlitpuZmEELGl33BxMMmv_NbGhJhaDWVoICm6sSAs

Here is instruction: use msc.sh then on PC in disk manager right click
on disk and click online(it will wipe primary gpt table in lun0). now in
recovery use "gdisk /dev/block/sda" (\\.\physicaldrive# where # your drive number in windows disk manager) and these commands "r, c, y, w
and y" it will restore gpt table, after reconnecting phone to pc it will show that disk is active.

### Diskpart
>  [!WARNING]
> DO NOT ERASE ANY PARTITION WHILE IN DISKPART!!!! THIS WILL ERASE ALL OF YOUR UFS!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for taking the device to Samsung or flashing it with EDL (which doesn't even exist on Samsung devices), both of which will likely cost money)

```cmd
diskpart
```

#### Finding your phone
> This will list all connected disks
```cmd
lis dis
```

#### Selecting your phone
> Replace $ with the actual number of your phone (it should be the last one)
```cmd
sel dis $
```

#### Listing your phone's partitions
> This will list your device's partitions
```cmd
lis par
```

### Selecting the ESP partition
> Replace $ with the partition number of ESP (should be 30)
```cmd
sel par $
```

#### Formatting ESP drive
```cmd
format quick fs=fat32 label="ESPWINNER"
```

#### Add letter to ESP
```cmd
assign letter y
```

### Selecting the WinPE partition
> Skip this step if you are not using WinPE
> 
> Replace $ with the partition number of WinPE (should be 31)
```cmd
sel par $
```

#### Formatting WinPE drive
```cmd
format quick fs=ntfs label="WINPE"
```

#### Add letter to WinPE
```cmd
assign letter r
```

### Selecting the Windows partition
> Replace $ with the partition number of Windows (should be 31, or 32 if you are using WinPE)
```cmd
sel par $
```

#### Formatting Windows drive
```cmd
format quick fs=ntfs label="WINWINNER"
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, then replace `index:6` with the actual index number of Windows 11 Pro in your image

#### Installing drivers
> Replace `<winnerdriversfolder>` with the location of the drivers folder
```cmd
driverupdater.exe -d <winnerdriversfolder>\definitions\Desktop\ARM64\Internal\winner.txt -r <winnerdriversfolder> -p X:
```

#### Create Windows bootloader files
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Enabling boot menu
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" displaybootmenu yes
```

#### Disabling boot status policy
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" bootstatuspolicy IgnoreAllFailures
```

### Reboot to Android
> To set up dualboot

## [Last step: Setting up dualboot](/guide/dualboot.md)










