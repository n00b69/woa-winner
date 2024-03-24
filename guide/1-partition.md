<img align="right" src="https://github.com/n00b69/SAMSUNG-WINNER-WindowsARM/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Partitioning your device

### Prerequisites
- A brain (most important of all)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP]() FILE NEEDED

- [Parted]() FILE NEEDED


### Notes
> [!WARNING]  
> Do not run the same command twice unless specified.
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woa_msmnile_issues).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Flash TWRP with Odin
> If you already have TWRP installed, boot to it

#### Unmount all partitions
Go to TWRP settings and unmount all partitions

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

## FOR USERS WITH WINPE
> Skip to "FOR USERS WITHOUT WINPE" if you don't want to use WinPE

#### Creating ESP partition
```cmd
mkpart esp fat32 9730MB 10.2GB
```

#### Creating WinPE partition
```cmd
mkpart pe fat32 10.2GB 25GB
```

#### Creating Windows partition
```cmd
mkpart win ntfs 25GB 312GB
```

#### Recreating userdata
```cmd
mkpart userdata ext4 312GB -0MB
```

## FOR USERS WITHOUT WINPE
> Return "FOR USERS WITH WINPE" if you want to use WinPE

#### Creating ESP partition
```cmd
mkpart esp fat32 9730MB 10.2GB
```

#### Creating Windows partition
```cmd
mkpart win ntfs 10.2GB 312GB
```

#### Recreating userdata
```cmd
mkpart userdata ext4 312GB -0MB
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

















