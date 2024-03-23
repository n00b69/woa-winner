<img align="right" src="https://github.com/n00b69/SAMSUNG-WINNER-WindowsARM/blob/main/winner.png" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F

## Driver updating

#### Start TWRP recovery through the PC Odin 

> If you already have TWRP installed, just hold the power and vol+ buttons at startup


## Push script

```cmd
adb push msc /sbin
```

### Execute script

```cmd
adb shell sh /sbin/msc
```

## Assign letters to disks

#### Start the Windows disk manager

> Once the X3 Nfc is detected as a disk

```cmd
diskpart
```


### Assign `x` to Windows volume

#### Select the Windows volume of the phone
> Use `list volume` to find it, it's usually the one before the last

```diskpart
select volume <number>
```

DISKPART> sel par 30 yor partition
# Select the ESP partition, in this case it's 0 for our device

DO NOT EXECUTE THE FOLLOWING COMMAND IF YOU ONLY WANT TO MOUNT PARTITIONS
DISKPART> format quick fs=fat32 label="System"
# Format ESP as fat32

DISKPART> assign letter="X"
# Assign drive letter

DISKPART> sel par 31 yor partition
# Select Windows partition, in this case it's 31 for our device

DO NOT EXECUTE THE FOLLOWING COMMAND IF YOU ONLY WANT TO MOUNT PARTITIONS
DISKPART> format quick fs=ntfs label="WinWinner"
# Format Windows partition as NTFS

DISKPART> assign letter="R"
# Assign drive letter

DISKPART> exit


# Install Drivers

> Replace `<winnerdriversfolder>` with the location of the drivers folder

> Open cmd as administrator


```cmd
.\driverupdater.exe -d <winnerdriversfolder>\definitions\Desktop\ARM64\Internal\winner.txt -r <winnerdriversfolder> -p X:
```


##### Boot with Windows bootable UEFI image #####

```
Flash uefi image samsung_winner.img via TWRP
```

  
  

# Finished!
