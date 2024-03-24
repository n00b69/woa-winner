<img align="right" src="https://github.com/n00b69/SAMSUNG-WINNER-WindowsARM/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Driver updating

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)
  
- [Drivers]() FILE NEEDED

- [Modded TWRP](https://mega.nz/file/LoVGETDK#-lwSOZeVRTuyOYOOv84RqhZJs8Ns-ESpoM6cT6-X-Kg) (should already be installed)

### Boot to the modded TWRP
> Flash it in Odin if you don't have it installed for whatever reason

#### Running the msc script
```cmd
adb shell msc.sh
```

### Diskpart
```cmd
diskpart
```

#### List device volumes
> To print a list of all the connected volumes, run
```cmd
list volume
```

#### Select Windows volume
> Replace $ with the actual number of **WINWINNER**
```cmd
select volume $
```

#### Assign letter to WINWINNER
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> Enter the drive letter of `WINWINNER`, which should be X, then press enter

### Boot back into Windows
> Reboot your device to boot back into Windows. If this boots you to Android, reflash the UEFI image through fastboot or by using the WOA Helper app

  
  

# Finished!
