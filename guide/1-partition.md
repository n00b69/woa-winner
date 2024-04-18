<img align="right" src="https://github.com/n00b69/woa-winner/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Partitioning your device

### Prerequisites
- A brain (most important of all)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Modded TWRP](https://github.com/n00b69/woa-winner/releases/tag/Recovery)

- [Parted](https://github.com/n00b69/woa-beryllium/releases/download/Files/parted)


### Notes
> [!WARNING]  
> Do not run the same command twice unless specified.
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woa_msmnile_issues).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Flash the modded TWRP
> If you have the official TWRP installed, flash it through there. Otherwise use Odin.

#### Unmount all partitions
Go to TWRP > Mount > and unmount all partitions

#### Running parted
> Download the parted file and move it in the platform-tools folder, then run
```cmd
adb push parted /sbin && adb shell "chmod +x /sbin/parted" && adb shell /sbin/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **30**
```cmd
rm $
```

#### Creating ESP partition
```cmd
mkpart esp fat32 9730MB 10.2GB
```

#### Creating Windows partition
> Replace **300GB** with the value you want to be allocated to Windows
```cmd
mkpart win ntfs 10.2GB 300GB
```

#### Creating WinPE partition
> [!Note]
> This is optional

> Replace **300GB** with the end value of Windows
>
> Replace **300GB** with the end value you want WinPE to have
```cmd
mkpart win ntfs 300GB 325GB
```

#### Recreating userdata
> Replace **300GB** with the end value of the Windows or WinPE partition you created above
```cmd
mkpart userdata ext4 300GB 512GB
```

#### Make ESP bootable
> Replace **$** with the number of the **ESP** partition, which should be **30**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

#### Format data
Go to the Wipe menu and press Format Data, 
then type `yes`.

### Check if Android still starts
Restart the phone, and see if Android still works

## [Next step: Installing Windows](2-install.md)

















