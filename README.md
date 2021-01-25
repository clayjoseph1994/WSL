# WSL
Different options for WSL (specifically version 2)

We want WSL2, Windows Terminal, and a distro of choice from the Windows Store (I am using Kali)
This guide has a lot of the info needed to make this work:
https://yduman.github.io/blog/wsl2-setup/

The sh file in this repo has the script that needs to be run to get the fonts working properly in Windows Terminal and WSL2


Add WinKex to have Kali GUI over VNC:
https://www.kali.org/docs/wsl/win-kex/

In the Kali WSL2 instance, run:
sudo apt update && sudo apt install kali-win-kex

Win-KeX supports three modes:
1- To start Win-KeX in Window mode with sound support, run:
kex --win -s

2- To start Win-KeX in Enhanced Session Mode with sound support and arm workaround, run:
kex --esm --ip -s

3- To start Win-KeX in Seamless mode with sound support, run:
kex --sl -s



ADD WINDOWS TERMINAL SHORTCUT-------
Advanced Win-KeX in window mode with sound - Kali icon and start in kali home directory:
Copy the kali-menu.png icon across to your windows picture directory and add the icon and start directory to your WT config (From Windows Terminal, ctrl + ,:

{
        "guid": "{55ca431a-3a87-5fb3-83cd-11ececc031d2}",
        "hidden": false,
      "icon": "file:///c:/users/<windows user>/pictures/icons/kali-menu.png",
        "name": "Win-KeX",
        "commandline": "wsl -d kali-linux kex --wtstart -s",
      "startingDirectory" : "//wsl$/kali-linux/home/<kali user>"
},
  
Save this config file then check the dropdown in Windows Terminal and you should see "Win-KeX" as an option.
CLick it then a prompt will come up requesting admin permission. Allow this, then follow prompts in temrinal screen:
-Enter and verify a password
-Decide whether you want a view-only password

Once you do this it should boot into KeX. If you're like me, the window will take over your screen and you can't click anywhere.
Press F8 and then uncheck full screen from the menu.
Now I see a prompt saying "Unable to contact settings server- Failed to execute child process "dbus-launch" (no such file or directory)
Go ahead and close the KeX window

Thank god for google. I found this link: https://www.reddit.com/r/Kalilinux/comments/jt7k6c/kali_linux_gui_on_wsl2_error_when_using_kaliwinkex/
A user with the name lgeorgiadis stated that running a command made it work for them
Go back to your kali WSL2 window and type: sudo apt-get install dbus-x11
Enter your password
Let that finish downloading
Restart your KeX session in Windows Terminal

VOILA! Kali with the GUI working on Windows 10 using WSL2!

For extra fun (if you have the storage space) go ahead and run: sudo apt install kali-linux-large
This will install the large package of kali with a lot of the commonly used tools to beef up your distro

If you also want ZSH in Kali, go ahead and download gnome terminal:
sudo apt install gnome-terminal

Then open settings manager in kali
Navigate to Default Applications
Click the utilities tab
Change the default terminal emulator to GNOME Terminal

Close your existing terminal, then open terminal again
Enter: sudo apt-get install zsh
Then: chsh -s $(which zsh)
Right click in the terminal and select Preferences from the menu
Click the command tab 
Click the checkbox for run a custom command instead of my shell
Type "zsh" in the input box next to "Custom Command:"
Nothing will have seemed to change, but you have to close your existing terminal and restart it to see the changes
Now type: echo $SHELL






Happy Tweaking!







