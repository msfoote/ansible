# Windows 11 Setup

## Installation

Load the ISO file or Plug in the USB. Hit a key after boot

Wait for the installation screen to appear

![Installation Start](https://i0.wp.com/www.kadvacorp.com/wp-content/uploads/2021/06/setup11-start-edited.jpeg?resize=692%2C590&ssl=1)

Click `Next` and then `Install now`

When it asks to Activate Windows click on `I don't have a product key`

It will then offer a list of operating systems to install. Select `Windows 11 Pro`

Then accept the license and click `Next`

Click on `Custom: Install Windows only (Advanced)`

![Custom Install](https://filestore.community.support.microsoft.com/api/images/ff7c1bf5-d644-4caf-bb5d-6c7d7426368d)

At this point the instructions diverge a bit depending on the installation target.

### Virtual Machine - skip to [Bare Metal](#bare-metal---skip-to-virtual-machine)

In a virtual machine environment unless you have passed hardware directly to the virtual machine you will see no drives. You will need to utilize the [latest VirtIO drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso).

Click on `Load driver` then click on `Ok`.

A list of drivers will be shown and you should select the one that says `W11` in the path and click `Next`

![Virtio Driver](https://www.aih.app/wp-content/uploads/2023/02/image-91.png)

Once the machine is done you will see a `Drive 0 Unallocated Space`. Click on that and then click `Next`

[Skip to next step](#installation-copies-files)

### Bare Metal - skip to [Virtual Machine](#virtual-machine---skip-to-bare-metal)

```In a virtual machine environment unless you have passed hardware directly to the virtual machine you will see no drives. You will need to utilize the [latest VirtIO drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso).

Click on `Load driver` then click on `Ok`.

A list of drivers will be shown and you should select the one that says `W11` in the path and click `Next`

![Virtio Driver](https://www.aih.app/wp-content/uploads/2023/02/image-91.png)

Once the machine is done you will see a `Drive 0 Unallocated Space`. Click on that and then click `Next`
```

### Installation Copies Files

At this point the Installer will copy all of the necessary files and will then reboot. Be patient as it may reboot several times and you may have to reset it if it gets stuck.

Eventually it will open to a screen asking for your country or region.

![Country_Region](https://www.wpxbox.com/img/2021/08/Windows-11-Setup-Screen.png?ezimgfmt=ng:webp/ngcb15)

Choose `United States` and click `Yes`

Choose `US` and click `Yes`. `Skip` adding an additional layout

### Bypass Network Installation

Windows 11 forces users to login with a Windows Live account but we can bypass this. Depending on the method of installation the instructions diverge a bit.

### Windows Asks You to Connect to a Network

If you see an option of `I don't have internet` then skip to [Windows Asks You to Connect to a Network Part 2](#windows-asks-you-to-connect-to-a-network-part-2)

To bypass this option we will perform the following procedure.

Press `Shift + F10` which will open up a command prompt/terminal

Type in

```powershell
OOBE\BYPASSNRO
```

This will reboot the computer once again and start you back at the point of asking for your country/region. Follow the steps above and then move onto [Windows Asks You to Connect to a Network Part 2](#windows-asks-you-to-connect-to-a-network-part-2)

### Windows Asks You to Connect to a Network Part 2

![Skip Internet](https://filestore.community.support.microsoft.com/api/images/0dc02787-ce2e-4dac-858e-d74cd2d98ed5?upload=true&fud_access=wJJIheezUklbAN2ppeDns8cDNpYs3nCYjgitr%2bfFBh2dqlqMuW7np3F6Utp%2fKMltnRRYFtVjOMO5tpbpW9UyRAwvLeec5emAPixgq9ta07Dgnp2aq5eJbnfd%2fU3qhn5498QChOTHl3NpYS7xR7zASsaF20jo4ICSz2XTm%2b3GDR4XitSm7nHRR843ku7uXQ4oF6innoBxMaSe9UfrAdMi7owFKjdP9m1UP2W5KAtfQLOmJj50HWzKvptzhhCuhgPoNjAbdXdG1UAttuAnuN%2bw5exSpm1oiXcwiWOZx9uJxFEgpP7%2fQ5cmYTr4kDFMq1cl22GXpSonffwC45dMRa07GxyqjGptkox7UtK8SNY7ZpKqFMkqP1d8qOPVNKCc33lzzzLTl3ka9L2sOEd3FO76Qw%2fgel%2bZOUOHLYhR1hohMVg%3d)

Click on the option `I don't have internet` and then `Continue with limited setup`

### Normal Installation

Create a user account with your name, a password and 3 security questions.

You will then be asked about privacy settings. Disable them to your liking and click `Accept`

The setup will then proceed with customizing the system. It will tell you 'This might take a few minutes'

You will then be presented with your desktop.

### Final Virtual Machine Configuration

If you are working on a bare metal machine proceed to [Setup the PC](#setup-the-pc-for-external-control)

Open up File Explorer and navigate to the CD Drive named `virtio-win-xx`

Run the `virtio-win-gt-x64` installer. This will install drivers for all of the virtualized hardware that is being used.

Once you are presented with a completion window click `Finish`. Notice that you should have network access unless you specifically excluded network devices from the virtual machine

### Continue Following Guide on the New PC

Open up Microsoft Edge and Sign In.

Set your default theme and Finish the setup.

### Setup the PC for External Control

We need to setup OpenSSH to allow for the PC to be controlled remotely.

We will install [Chocolatey](https://chocolatey.org/install#individual) which is a package manager and then install OpenSSH.

Right click on the Windows Icon and select `Windows PowerShell (Admin)`. This will open up a terminal window.

Paste the following command into the terminal.

```PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Once that completes type the following to setup OpenSSH

```PowerShell
choco install openssh -params="/SSHServerFeature" -y
```

The final thing to do is to determine the IP Address of the machine.

```PowerShell
ipconfig
```

The data that is reflected on the line beginning with `IPv4 Address` is what we need and should look like `192.168.1.XXX`

```PowerShell
IPv4 Address.  .  .  .  .  .  .  .  .  :  192.168.1.XXX
```

The very last thing that needs to be done is a file needs to be created with the contents of the public SSH key we will use to control it.

The file is located at `C:\ProgramData\ssh\administrators_authorized_keys`

You can use the following commands to transfer the key from a master windows system to your new system.

```PowerShell
# Get the public key file generated previously on your client
$authorizedKey = Get-Content -Path $env:USERPROFILE\.ssh\id_rsa.pub

# Generate the PowerShell to be run remote that will copy the public key file generated previously on your client to the authorized_keys file on your server
$remotePowershell = "powershell Add-Content -Force -Path $env:ProgramData\ssh\administrators_authorized_keys -Value '$authorizedKey';icacls.exe ""$env:ProgramData\ssh\administrators_authorized_keys"" /inheritance:r /grant ""Administrators:F"" /grant ""SYSTEM:F"""

# Connect to your server and run the PowerShell using the $remotePowerShell variable
ssh username@ipaddress $remotePowershell
```

From here we can move to our Ansible machine to finish configuration.
