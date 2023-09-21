[//]: # (This Source Code Form is subject to the terms of the Mozilla Public)
[//]: # (License, v. 2.0. If a copy of the MPL was not distributed with this)
[//]: # (file, You can obtain one at https://mozilla.org/MPL/2.0/.)

# firefox-dev.desktop
Setting up Firefox Developer Edition in Ubuntu

Download the latest [Firefox Developer Edition here](https://www.mozilla.org/en-US/firefox/developer/)

Unpack the Tar file under the /opt directory, now we won't delete it by accident

```bash
cd ~/Downloads
sudo tar xjf firefox-*.tar.bz2 -C /opt/
```

We can now savly remove the Tar file

```bash
rm -r firefox-*.tar.bz2
```

Creating a symlink of the executable to open it globally from the terminal

```bash
sudo ln -s /opt/firefox/firefox /usr/local/bin/firefox-dev
```

Now we can open the browser with:

```bash
firefox-dev
```

Lets create a desktop shortcut



We can [download this version](Firefox-dev.desktop)

Or copy pasta it your self via:
```bash
nano Firefox-dev.desktop
# ^ note that you can use an other editor if you want
```

To be able to find Firefox Developer Edition in our application tray use:

```bash
sudo cp Firefox-dev.desktop /usr/share/applications/
```

To add a shortcut on the desktop we need to do the following:

```bash
cp Firefox-dev.desktop ~/Desktop/
gio set ~/Desktop/Firefox-dev.desktop metadata::trusted true
chmod a+x ~/Desktop/Firefox-dev.desktop
```
