<img align="right" src="(https://www.zeebiz.com/technology/mobiles/news-bad-news-for-galaxy-fold-owners-samsung-sounds-death-knell-for-this-feature-205199)" width="164" alt="Windows 11 Running On SAMSUNG winner F900F">


# Running Windows on the SAMSUNG GALAXY FOLD WINNER F900F

## Installation

> You will need to have MTP disabled in Mount


## Push necessary tools:
```cmd
adb push msc.sh /sbin
```

### Execute the msc script

```cmd
adb shell sh /sbin/msc.sh
```

##  Correct disk mapping in Windows disk manager 
https://sourceforge.net/projects/gptfdisk/files/gptfdisk/
https://mega.nz/file/K5UkQLrC#vCwlitpuZmEELGl33BxMMmv_NbGhJhaDWVoICm6sSAs

Here is instruction: use msc.sh then on PC in disk manager right click
on disk and click online(it will wipe primary gpt table in lun0). now in
recovery use "gdisk /dev/block/sda" (\\.\physicaldrive# where # your drive number in windows disk manager) and these commands "r, c, y, w
and y" it will restore gpt table, after reconnecting phone to pc it will show that disk is active.

## Assign letters to disks
  

#### Start the Windows disk manager

> Once the inner is detected as a disk

```cmd
diskpart
```


### Assign `X` to Windows volume

#### Select the Windows volume of the phone
> Use `list volume` to find it, it's the ones named "WINWINNER" and "ESPWINNER"

```diskpart
select volume <number>
```

#### Assign the letter X
```diskpart
assign letter=x
```

### Assign `X` to esp volume

#### Select the esp volume of the phone
> Use `list volume` to find it, it's usually the last one

```diskpart
select volume <number>
```

#### Assign the letter R

```diskpart
assign letter=r
```

### Exit diskpart:
```diskpart
exit
```

  
  

## Install

> Replace `<path/to/install.wim>` with the actual install.wim path,

> `install.wim` is located in sources folder inside your ISO
> You can get it either by mounting or extracting it

```cmd
dism /apply-image /ImageFile:<path/to/install.wim> /index:1 /ApplyDir:R:\
```

# Install Drivers

> Replace `<winnerdriversfolder>` with the location of the drivers folder

```cmd
driverupdater.exe -d <winnerdriversfolder>\definitions\Desktop\ARM64\Internal\winner.txt -r <winnerdriversfolder> -p X:
```

  

# Create Windows bootloader files for the EFI

```cmd
bcdboot X:\Windows /s R: /f UEFI
```
# R: is the assigned letter for the Windows partition
# X: is the assigned letter for the EFI partition
# if you use different ones, be sure to replace them!
    

# Allow unsigned drivers

> If you don't do this you'll get a BSOD

```cmd or PowerShell with admin privileges
bcdedit /store BCD /set "{default}" testsigning on
bcdedit /store BCD /set "{default}" nointegritychecks on
bcdedit /store BCD /set "{default}" recoveryenabled yes
bcdedit /store BCD /set "{bootmgr}" displaybootmenu yes
bcdedit /store BCD /set "{default}" bootstatuspolicy IgnoreAllFailures
```
### Enable usb c port

run regedit in your pc
reg load HKLM\OFFLINE R:\Windows\System32\Config\System
regedit
In HKEY_LOCAL_MACHINE/OFFLINE/ControlSet001/Control/USB/OsDefaultRoleSwitchMode change value to 1 After, in the command line of your PC, enter reg unload HKLM\OFFLINE Done!

# Boot into Windows

### Move the `<uefi.img>` file to the device

```cmd
adb push <uefi.img> /sdcard
```


### Flash the uefi image from TWRP
Navigate to the `uefi.img` file and flash it into boot

# Boot back into Android
> Use your backup boot image from TWRP

# Finished!
