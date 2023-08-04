Windows:
	- Rename Computer
	- Update Windows
	- Update Optional Windows Updates
	- Add a printer
	- Run autologon (after chocolatey base.config install)

MS Edge:
	- Login to MS Edge
	- Login to plugins
	- Change default search engine to google

Install Chocolatey:
	- Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

Install via choco:
	- Baseline
  		choco install base.config -y
	- Gaming
  		choco install gaming.config -y
	- iOS Backups
  		choco install ios_backup.config -y

Nextcloud Client:
	- Open and log into Nextcloud client

Git
	- Configure identity
		git config --global user.email "matthew.foote@gmail.com"
		git config --global user.name "Matthew Foote"

Autohotkey
	- Git Clone Autohotkey repository
		git clone https://github.com/msfoote/autohotkey.git
	- Enter `shell:startup` into the Run prompt (WIN + R)
	- Copy link of Script to new folder


File Explorer:
	- Enable viewing of hidden files in File Explorer
	- Enable network discovery
	- Pin //FOOTEPRINT to Quick Access Bar
	- Unhide extensions for known file types

f.lux
	- Configure location

winscp
	- Show hidden files

Windows Personalization:
	- Change to Dark Mode
	- Set display setting appropriately

discord
	- Set to start at startup
	- Set to start minimized

VSCode:
	- Enable autosaving

Steam:
	- Log into steam using Steamguard on Phone
	- Download Games

Phone Link:
	- Add my phone

Pin Apps to Taskbar:
	- Steam
	- Phone Link
	- Cheathappens Auroroa

SSH:
	- Create SSH Kepair and send to other PCs
	- Or copy existing SSH Keys to C:\Users\matthew\.ssh and C:\ProgramData\.ssh
		- Taken from [https://sbytestream.pythonanywhere.com/blog/Import-ssh-keys-for-Git](https://sbytestream.pythonanywhere.com/blog/Import-ssh-keys-for-Git)

Remote Desktop Settings: Enable

Software Installs:
	- Cheathappens - Aurora: https://www.cheathappens.com/
	- PDF-XChange Editor Plus:
		- Check for new versions
		- Save new version and install from: \\FOOTEPRINT\Software\Utilities\PDF-XChange.Editor.Plus.v8.0.343.0

[Windows VM]
  Software Installs:
    - Quicken:
      - https://www.quicken.com/
    - Fujitsu Scansnap Software:
      - \\192.168.1.100\Software\Utilities\Fujitsu ScanSnap S1500M Software
      - Ensure Device is mapped to VM
    - iMazing:
      - Enter License number
      - Ensure USBs routed to VM
    - Brother QL-570
      - https://support.brother.com/g/b/downloadtop.aspx?c=us&lang=en&prod=lpql570eus
      - Old copies saved at \\192.168.1.100\Software\Utilities\Brother QL-570 Software
      - Ensure Device is mapped to VM
