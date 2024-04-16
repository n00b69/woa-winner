<img align="right" src="https://github.com/n00b69/woa-winner/blob/main/winner.png" width="350" alt="Windows 11 running on winner">

# Running Windows on the SAMSUNG GALAXY FOLD SM-F900F












### Diskpart
```cmd
diskpart
```

#### Select 

#### Add letter to Windows
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

#### Formatting Windows
> Go to Windows Explorer > This PC and select **WINWINNER**. Right click and format as NTFS.

### Installing Windows
> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)
```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, then replace `index:6` with the actual index number of Windows 11 Pro in your image

### Installing Drivers


### Boot into Windows
Reboot your phone. If you end up in Android instead of Windows, flash the UEFI again using WOA Helper.

#### Setting up Windows
> Your device will now set up Windows. This will take some time. It will eventually reboot, and after that the initial setup (oobe) should launch.

> [!Note]
> To skip the Microsoft Account login, use "g" for the email and password. Windows will then let you make a local account

## Finished!

















