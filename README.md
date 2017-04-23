# Desktop files for Qubes tools

The freedesktop
[Desktop Entry specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)
provides a standard for applications to integrate into a desktop environment.
Desktop entries are the configuration files that describe how an application
is launched and which data it can handle.
They also configure how an application appears in a menu with an icon, which
is subject to the related
[menu specification](https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html)
standard.

In [Qubes OS](https://www.qubes-os.org/) proper Desktop Entry settings help
you to prevent from accidentally opening suspicious files or URLs in a
privileged VM.

## qvm-open-in-dvm.desktop

A Desktop file for opening *local files* with qvm-open-in-dvm.

## qvm-browse-in-dvm.desktop

A Desktop file for opening *URL schemas* with qvm-open-in-dvm.

## Installation

The Desktop files are meant to be placed in ~/.local/share/applications or
/usr/share/applications.

To get the correct icon, copy /usr/share/qubes/icons from dom0 to the AppVM's
/usr/share/icons/Qubes.

## Usage

Depending on the file manager, there are different ways to set the
default application.
Here are some examples.

### Thunar (local files)

In the AppVM's Thunar window, right click the file you want to open, select
"Open in Disposable VM", and check the "Use as default for this kind of file"
box.

### Nautilus (local files)

In the AppVM's Nautilus window, right click the file you want to open, select
the "Open With" tab, select "Open in Disposable VM", and click the "Set ad
default" button.

### Xdg-settings (URL schemas)

In the AppVM's terminal window, set the default browser:

~~~
xdg-settings set default-web-browser qvm-browse-in-dvm.desktop
~~~

### Checking the Desktop Entry settings

You can check the Desktop Entry setting for any file with the following
command:

~~~
xdg-mime query default $(mimetype <file>|awk '{print $2}')
~~~

The output (for any suspicious file type) should be "qvm-open-in-dvm.desktop".

Check the default browser setting with:

~~~
xdg-settings get default-web-browser
~~~

The output should be "qvm-browse-in-dvm.desktop".
