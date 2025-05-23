# **steam-windows-emulation**

Tutorial on how to use Steam for Linux as a Windows emulator.

## Overview

Steam is a digital content distribution service developed by Valve.
As most games are developed for the Windows platform, Valve created
an open-source tool called Proton for the Steam Linux client.
Proton acts as Windows compatibility layer for Linux, allowing games
exclusive to Windows to run on Linux.

While Proton was developed for allowing Windows games to run on Linux,
it can also be used to to run *any* type of Windows software,
from games to productivity applications.
This allows Steam for Linux to serve as a Windows emulator that is easy
to setup and configure.

This tutorial will demonstrate this capability by using Steam for Linux
to install and configure Notepad++, a popular Windows text editor.

## Level One: Installation

### Prerequisites

Before we begin, you will need to have:

* The Steam for Linux client installed
* Downloaded the Windows `.exe` installer for your application

### Installing the Program

In the Steam client, select `Games > Add a Non-Steam Game to My Library`
from the menu:

`IMAGE`

The window `Add Non-Steam Game` will pop up. Select the `Browse…` button:

`IMAGE`

Navigate to the location of your Windows `.exe` installer and select it.
You can filter the list in the `Add Non-Steam Game` window by entering
the name of the installer in the text field. Once you have ensured your
installer is checked, click the `Add Selected Programs` button:

`IMAGE`

This will add the installer to your Games list on the left side of your
Library. Before you launch the installer, right-click it and select
`Properties…`:

`IMAGE`

A properties window will pop up.
Click on the `Compatibility` section on the left side.
Check the `Force the use of a specific Steam Play compatibility tool` option
and select from the drop-down the latest stable version of Proton.
At the time of this writing, this version is `Proton 9.0-4`:

`IMAGE`

When you are done, close the window and launch the program.
The installer for your selected application should appear:

`IMAGE`

If for some reason the installer does not launch, try a different version of
Proton. Once the installation process is complete, your should see your
program successfully launch:

`IMAGE`

Although the program launched, the shortcut still points to the installer.
Next, we will need to modify the properties so that the shortcut launches
the installed program.

## Level Two: Configuration

### Locate the installed application

First you will need to locate where the application was installed.
When you add an application to Steam, the files for that application
are placed in a subdirectory located at:

```
~/.local/share/Steam/steamapps/compatdata/
```

However, these subdirectories are named with numerical IDs rather than the
application name. You will need to identify which subdirectory contains the application
you just installed. The easiest method will be to use the `find` command
from the terminal. To do this, first navigate to the parent directory:

```
cd ~/.local/share/Steam/steamapps/compatdata/
```

Then use the `find` command with the name of your application:

```
find . -iname '*notepad++*'
```

If this does not reveal the location, you will need to manually search for the
directory. Since we just installed the application,
you can narrow down your search by checking the creation timestamps
of the subdirectories by running:

```
ls -l --time=creation
```

As an example, my Notepad++ installation was placed in a directory named `3060847736`
and I found the `.exe` for the application at:

```
~/.local/share/Steam/steamapps/compatdata/3060847736/pfx/drive_c/Program Files/Notepad++/notepad++.exe
```

Once you have found the correct location for the `.exe` of the application,
continue on to the next step.

### Modify the shortcut properties

Close out the application if you have not done so already.
As before, right-click the entry for your application in the Games list
on the left side of your Library and select `Properties…`:

`IMAGE`

We will need to point the shortcut to the actual location of the installed
Windows program.

In the `TARGET` field, enter the full path to the `.exe` enclosed in quotes:

```
"/home/user/.local/share/Steam/steamapps/compatdata/3060847736/pfx/drive_c/Program Files/Notepad++/notepad++.exe"
```

In the `START IN` field, enter the directory containing the `.exe` enclosed in quotes:

```
"/home/user/.local/share/Steam/steamapps/compatdata/3060847736/pfx/drive_c/Program Files/Notepad++"
```

You can also modify the name of the shortcut at the top to reflect the application name.
When you are done, your `Shortcut` section should look similar to the following:

`IMAGE`

### Launch the application

Close out the properties window and launch the application.
If you configured everything correctly, the application should run:

`IMAGE`

And you are done! However, if you are like me and find yourself squinting
to read the text in the application, you may want to continue on to the
next step.

## Level Three: DPI Scaling

## Level Four: Symlinks

## License

GNU General Public License v3.0

## References

