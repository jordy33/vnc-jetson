### How to install VNC in jetson nano

Install vino
```
sudo apt update
sudo apt install vino
gsettings set org.gnome.Vino prompt-enabled false
gsettings set org.gnome.Vino require-encryption false
```

Find ethernet UUID
```
nmcli connection show
```

Add the UUID to vino-server enabled-connections.
```
dconf write /org/gnome/settings-daemon/plugins/sharing/vino-server/enabled-connections "['<UUID of the ethernet>']"dconf write /org/gnome/settings-daemon/plugins/sharing/vino-server/enabled-connections "['856c1130-6337-391d-bddc-676ca8c98cf0']"
```
Open the schema in your favourite editor,
```
sudo vi /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
```

and go ahead and add the following key into the XML file.
```
sudo glib-compile-schemas /usr/share/glib-2.0/schemas
```

So go ahead and click on the “Settings” icon, and then the “Desktop Sharing” icon which is in the top row.
```
Sharing:
Enable: Sharing Allow other users to view your destop
Enable: Allow other users take control your deskto

Security:
Enable: Require the user to enter this password: <capture password>

Show Noticiation Area Icon
Select: Only when someone is connected

```

In search panel. Type ‘startup applications’ into the search box that appears at the top of the screen.
Click add and put:
```
Name: Vino
Command: /usr/lib/vino/vino-server
Comment: VNC Server
```

### Reboot Jetson Nano


In the Client Side Install : Real VNC client

[[here](https://www.realvnc.com/en/connect/download/viewer/linux/)]

Create a startup script to fix resolution
```
#!/bin/bash
xrandr --fb 640x920
```
