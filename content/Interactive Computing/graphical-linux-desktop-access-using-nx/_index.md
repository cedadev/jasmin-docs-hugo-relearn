---
aliases: /article/4810-graphical-linux-desktop-access-using-nx
categories:
- Interactive Computing
- Software on JASMIN
collection: jasmin-documentation
date: 2023-06-08 16:26:34
description: Graphical linux desktop using NoMachine NX
slug: graphical-linux-desktop-access-using-nx
tags:
- nx
- no machine
- nomachine
- x2go
- graphical
- desktop
- X11
- X
- gui
title: Graphical linux desktop using NoMachine NX
---

This article explains how to connect to a graphical linux desktop within the
JASMIN environment using NoMachine NX. It explains:

  * how using a JASMIN-side graphical desktop can improve performance
  * how to set up your connection using the NX enterprise client
  * how to log in and use a graphical desktop session

## Contents

  * Introduction
  * Installation of client
  * Setting up your connection
  * Connecting
  * Usage
  * Troubleshooting

# Introduction

Using graphical applications over a wide-area network can be very slow, and is
not recommended or supported on JASMIN. This service helps by providing a
graphical desktop **within** the JASMIN environment, instead of on the end
user's local machine at the end of a wide-area network path from JASMIN. A
small client application available for you to install on your local machine
enables you to connect to specific servers within JASMIN but send graphics
output across the network in compressed form, resulting in much better
performance.

Via a web browser provided on this graphical desktop, this service also
provides a means of accessing web-based resources within JASMIN which are not
otherwise visible outside.

The service provides an improved user experience compared to that offered by
the alternative X2GO system previously offered on JASMIN and is strongly
recommended over standard X11 graphics.

The following "special" login servers have the NX service available and can be
used as described below:

  * `nx-login1.jasmin.ac.uk`
  * `nx-login2.jasmin.ac.uk` ([Contingency config]({{< ref "login-servers#contingency-login-servers" >}}) similar to `login2.jasmin.ac.uk`, to make it available from clients without reverse DNS lookup to a domain in the JASMIN allow-list. Use this option if you need to connect from home and do not have an institutional VPN available)
  * `nx-login3.jasmin.ac.uk` ([Contingency config]({{< ref "login-servers#contingency-login-servers" >}}) as above) 
  * `nx-login4.jasmin.ac.uk` ([Contingency config]({{< ref "login-servers#contingency-login-servers" >}}) as above, but also supports users with usernames > 8 characters)

### Notes

  * In all other respects these are the same as the standard [login servers]({{< ref "login-servers" >}}), but should only be used by users connecting with the NX enterprise client as described below. Please do not use them for standard terminal-based SSH connections as this preserves system resources for their intended purpose.
  * Although the graphical desktop session which you create with this service should persist when you close the client (unless you specifically log out), you should not rely on this feature (so please don't report this as a problem: occasionally machines run out of resources and sessions get killed). Keeping sessions open consumes resources on the server even when you're not using the session, which may mean that other users can't use the service.
  * nx-login4 has been introduced to help cater for users whose usernames exceed 8 characters length. This works around a known limitation in the NX server software but may not solve the problem for users with very long names (created before we introduced a limit to prevent this happening: if this still affects you and you cannot make onward connections to other machines in NX, please contact the helpdesk)

# Installing NoMachine Enterprise Client

Download the appropriate version of the NoMachine Enterprise Client from
[NoMachine](https://www.nomachine.com/download-enterprise#NoMachine-
Enterprise-Client). This page contains links to several different products.
**The only one you need to install is "NoMachine Enterprise Client".**

Versions are available for Windows, Mac and Linux. You may need privileges on
your local machine in order to install the software so you may need to ask for
help from your local IT helpdesk.

Note that **"Nomachine Enterprise Client"** is a different application to the
"Nomachine Enterprise Desktop" available from the more publicised download
link on the NoMachine website or other applications in the NoMachine suite:
the desktop edition contains additional components to enable remote access to
your **own** (e.g. desktop) machine from a remote location: perhaps convenient
but not what we are trying to enable for you here.

The **NoMachine Enterprise Client** is purely a client to connect to a remote
server: in our case the server is at the JASMIN end, providing an additional
(graphical desktop) interface to JASMIN.

Remember to check for updates for the enterprise client to ensure you always
have the latest stable version. You can configure the application to check for
updates (and optionally apply them automatically) by going to Settings /
Updates in the menu.

# Setting up your connection

As you can see from the following videos, the instruction steps below are very
similar for Windows / Mac / Linux, once the enterprise client is installed.
Note that the interface may look slightly different depending on which version
number of the client you have installed (we can't promise to keep the videos
up to date with every new version, unfortunately!)

{{< youtube id="-O-Ec4lZJuE" title="Windows" >}}

***


{{< youtube id="R9zb3LbrlJE" title="Mac" >}}

***

{{< youtube id="g22dDHX7Tt0" title="Linux" >}}


Instructions for v7.x clients: (v6.x clients look slightly different hence
slightly different steps, but the same concept overall)

  1. Open the NX client 
      1. On Mac and Windows, click the NoMachine Icon
      1. On Linux, the default location for the executable once installed is `/usr/NX/bin/nxplayer`, so you may want to add this to your path. Your desktop environment may enable you to add an icon to your desktop. 
  1. In the "Machines" view, select "Add"
      1. You're now in the "Address" tab. Type a name for this connection profile, and the full hostname, e.g. `nx-login1.jasmin.ac.uk`. Set the Protocol to "SSH", which will change the port to 22. 
  1. Go to the "Configuration" tab.
      1. Choose **"Use key-based authentication with a key you provide"** , then click the Modify button to the right. 
      1. The default is "Use password authentication": this generally doesn't work so we don't support this.
      1. Use the button to the right to navigate to your private key, or type the path in the box. 
      1. Your private key may be in a hidden directory e.g. `~/.ssh` see Troubleshooting
      1. Make sure you tick the box "Forward Authentication" **IMPORTANT**
  1. Go back to the Address Tab
      1. Click Connect (top right) if all looks correct.
      1. You may find that it has now forgotten where you're private key is, if so **repeat steps 3 & 4**. [This was a bug in earlier versions!]
      1. Click "Connect" then follow the steps below in "Connecting".

#  Connecting

  1. Enter your JASMIN username and your SSH passphrase. Click OK
  2. Select "Create a new virtual desktop", click Continue
  3. **Note the instructions for how to reach the NX menu once in the session, and select screen settings from the list of icons: Recommended setting is "Fit to window" (leftmost icon)**
  4. Click OK on this and subsequent screens giving information about the NX and desktop environments.
  5. You should be presented with a linux deskop on the server to which you connected, e.g. `nx-login1.jasmin.ac.uk`
  6. Click "Activities" (top left menu on desktop) ![](file-XXVsbhxQi8.jpg)
  7. Open a terminal window by clicking the "Terminal" icon in the menu down the left hand side.  
  ![](file-chi3HNdvmk.jpg)

  8. To see the list of sci servers which is normally presented at login (which helps in selected a less-loaded sci server), type the following:  
  ```console
  cat /etc/motd
  ```  	

# Using the graphical desktop environment

Once you have set up the environment to your liking, you can

  * use the web browser on that system to access web-based resources available only within JAMSIN
  * make SSH connections to other systems within JASMIN such as `sci1.jasmin.ac.uk`
  * if necessary, use a graphical applications on other systems within JASMIN and send the output back to your graphical desktop.

  1. Click "Activities" (top left menu on desktop) 

![](file-XXVsbhxQi8.jpg)

  2. Click the Firefox icon in the side bar menu to start the Firefox web browser. Use this to access web-based resources only available within JASMIN. Do not use for personal web browsing. To toggle Firefox between taking up the whole of your desktop, and running in a smaller, sizeable window, double-click its title bar (this applies to any windowed application on the desktop). 

![](file-zykeLBbqgb.jpg)

  3. Click the Terminal icon 

![](file-RMJ4FzLkUz.jpg)

  4. Try an onward SSH connection, for example to a SCI machine. 
    
```console
ssh -AX <username>@sci1.jasmin.ac.uk
```
(where `<username>` should be replaced by your JASMIN username).

  5. Work interactively on a SCI machine as you would normally, but any graphical tools/applications should now work efficiently. 

  6. (Example of a graphical application on another machine within JASMIN). Try opening a simple graphical application on `sci1.jasmin.ac.uk` with the command:
    
  ```console
  xclock
  ```
  (you may find `-AY` works if `-AX` does not).

  You may also get a few warning messages like this, which can safely be
  ignored:

  ```
  Warning: Missing charsets in String to FontSet conversion
  ```

  Cancel the graphical application (xclock) with `CTRL + c`, or use the
  application's own exit command, if it has one.

  With other graphical applications opened on other servers within JASMIN, you
  may get warning/error messages like these as they start up: these can safely
  be ignored. Sometimes an application window can take a few seconds to appear,
  but should work normally after that.

```
Failed to open connection to "session" message bus: /usr/bin/dbus-launch terminated abnormally without any error message
Running without a11y support!
Gtk-Message: 08:58:38.169: Failed to load module "pk-gtk-module"
Gtk-Message: 08:58:38.171: Failed to load module "canberra-gtk-module"<br>
``` 	

  7. To log out of the virtual desktop, locate the menu top-right, and select your name, then "Log Out" 
    1. Don't worry if it appears that you're able to power off the machine with other users logged in: you would need administratrive privileges for this (which you don't have) so you can't do this accidentally. Please don't try, however!

## Notes

  * The number of "virtual desktops" which can be created per user is limited to 1 in order to preserve system resources.
  * Although in theory sessions and desktop windows should persist when you close down the NoMachine client and when you re-open it to the same connection, you should not rely on this feature. Keeping long-running sessions open reduces resources available to other users.
  * The option to shut down the machine does not work for a "regular" user (only admins). Please just "Log out" instead.

#

# Troubleshooting

### Authentication error (Windows users) 

* Try reformatting your private key using a tool available within MobaXterm. 
    * If you have tested and can successfully connect to `nx-login2.jasmin.ac.uk` from a MobaXterm terminal but **NOT** from the NoMachine NX client ("Authentication Failed"), then try following the steps below: these instructions are for Windows users.
    * Note that this doesn't make you a new key, it just makes a newly-formatted version of your key, which can sit alongside your existing private key file. The public key stays the same, so there's no need to upload anything new to your JASMIN profile.
    * Open the MobaKeyGen tool: MobaXterm menu / Tools / **MobaKeyGen (SSH Key Generator)**
    * Click Load, navigate to your existing private key file (you may need to change the filter to show all files (*.*) instead of just (*.ppk). Select your key, click Open
    * You will be prompted for the passphrase which you set when creating the key.
    * In the MobaKeyGen menu, select Conversions / Export OpenSSH key (the 2nd option)
    * Choose a new name for the file (it is recommended to just append something on to the end of your existing key name, so that it's clear that they are formats of the same key, e.g. id_rsa_jasmin -> id_rsa_jasmin_f (but the name is not significant).
    * Close the "MobaXterm SSH Key Generator" window
    * Make yourself a new NX connection profile, pointing to the new file
    * You should now be able to connect.
    * The following video shows this sequence in action (although the key is named slightly differently)

### Transposed symbol keys

After the first connection (particularly for Mac users), subsequent connections to the same connection profile sometimes have some symbols keys e.g. `@` and `"` transposed. 

Watch the following video for how to correct this.

{{< youtube bC41sdqOr7k >}}

Doing as shown leaves a small drop-down choice tool in your Gnome desktop menu so that you can correct the problem if it re-occurs later. The correct choice for the author's UK Mac was "English (UK, Macintosh)", but you may need to experiment with the choices available to match your own keyboard layout.

If you click the small keyboard-layout icon (bottom right when viewing the list of choices), you will be shown a preview of that keyboard layout to compare with your own. 

### Connection timeout

Please do not try and connect using the proprietary "NX" protocol. Select "SSH" as the protocol. If you mistakenly use "NX" as the protocol you may see an error similar to the following when you try to connect (The correct port for **SSH** connections is 22)

```
A connection timeout has occurred while trying to connect to 'nx-login1.jasmin.ac.uk' on port '4000'. The issue could either be caused by a networking problem, by a firewall or NAT blocking incoming traffic or by a wrong server address. Please verify your configuration and try again.
```        		

### Authentication method

Please use "Private key" as the authentication method, not "Authentication agent", as the former has been found to work more consistently and reliably, particularly for onward connections to other machines.

## Client version

Make sure you have installed and are using the most recent version of the [NoMachine Enterprise Client](https://www.nomachine.com/download-enterprise#NoMachine-Enterprise-Client) (not the NoMachine Enterprise Desktop or any other applications from NoMachine).

### Key format

If you created your SSH private key using the "PuTTYgen" application, and are getting "Authentication failed" for a key pair that you know works OK for simple terminal connections, it could be that you need to convert the private key to "OpenSSH format" for use here. By doing this you would be creating an alternately-formatted version of the same private key, so the public key stays the same (and you don't need to re-upload that to JASMIN).
  * Open PuTTYgen and "Load an existing private key file" (click "Load")
  * Ignore the notice about saving it in PuTTY's own format (this is not useful here) (click "OK")
  * In the PuTTYgen menu, select "Conversions", then "Export OpenSSH key"
  * Save the newly-formatted private key file locally. The passphrase needed to unlock it should not have changed.
  * Use this newly-formatted key file with NoMachine NX.
      
### Passphrase vs Password

Be sure to use the PASSPHRASE associated with your SSH private key, and not the PASSWORD associated with your JASMIN account, when prompted using the NX client.
    
### Can't find your private key?

The location of your private key on your local machine may be in a hidden directory for example `~/.ssh`. In order to navigate to it to provide the location when setting up your connection profile, you may need to enable the display of hidden directories/files in your local desktop environment first. On a Mac you can do this with the shortcut `cmd + shift + .`. In Windows this is under File Explorer / View / Hidden Items. It's also possible that your home directory itself (normally `/Users/<username>`) is not configured to be displayed by default in `Finder`. If this is case, go to Finder / Preferences / Sidebar / Show these items and tick the box next to the item representing your username: this should make it appear, and `.ssh` should be a subdirectory of this.
    
### Can't make an onward connection

Previous versions of the Windows client had problems with "forward authentication" enabled, but this is required for onward connection to other machines. If this happens, try:

* Does your username have > 8 characters? If so, try using `nx-login4`. 
* Uninstalling the v7 client client
* Deleting the `C:\Users\<username>\.nx` directory on your machine
* Re-installing and trying again.
* Deleting and making a new connection profile for the nx-login server you're connecting to.
    
### Can't display graphics from sci machine or other onward connection

Did you omit the -X option from the SSH command when you made the onward connection to that machine? Try -Y if -X doesn't work for you.

### Disk space

Check your disk usage in your JASMIN home directory: if this is over the 100G limit, you may not be able to write any temporary files and this could prevent NoMachine from being able to start a new session or even reconnect to an existing virtual desktop session. Clear out some space and re-check with `pdu -sh $HOME` to find out how much space you're using.

### "It worked yesterday"

For occasions where "it worked last time I tried to connect, but now doesn't", the time-honoured IT support advice of "turning it off and on again" is applicable: try restarting your local machine where the NX client is running, as this can sometimes clear issues with the client, your machine or your network connection. Don't forget to re-connect via your VPN if available.
