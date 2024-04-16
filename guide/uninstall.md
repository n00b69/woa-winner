<img align="right" src="https://github.com/n00b69/woa-winner/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Uninstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/n00b69/woa-winner/releases/tag/Recovery)

- [Parted](https://github.com/n00b69/woa-beryllium/releases/download/Files/parted)

### Boot into the modded TWRP
> Flash it with Odin if you haven't already

#### Unmount all partitions
Go to TWRP > Mount > and unmount all partitions

### Running parted
> Download the parted file and move it in the platform-tools folder, then run
```cmd
adb push parted /sbin && adb shell "chmod +x /sbin/parted" && adb shell /sbin/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions
```cmd
print
```

#### Removing Windows partitions
> Replace **$** with the actual number of the partitions
>
> Do this for every partition after **omr**
```cmd
rm $
```

#### Recreating the userdata partition
```cmd
mkpart userdata ext4 9730MB 512GB
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

## Finished!

















































