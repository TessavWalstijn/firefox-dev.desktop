[//]: # 'This Source Code Form is subject to the terms of the Mozilla Public'
[//]: # 'License, v. 2.0. If a copy of the MPL was not distributed with this'
[//]: # 'file, You can obtain one at https://mozilla.org/MPL/2.0/.'

# firefox-dev.desktop

Setting up Firefox Developer Edition in Ubuntu

> NOTE: I am now recommending to install Firefox via the .deb packages for Debian-based distributions
> The following instructions are from [Support Mozilla ¹](https://support.mozilla.org/en-US/kb/install-firefox-linux#w_install-firefox-deb-package-for-debian-based-distributions) with the settings v124 & Linux.

1. Create a directory to store APT repository keys if it doesn't exist:
   ```bash
   sudo install -d -m 0755 /etc/apt/keyrings
   ```
1. Import the Mozilla APT repository signing key:
   ```bash
   wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | gpg --dearmor | sudo tee /etc/apt/keyrings/packages.mozilla.org.gpg > /dev/null
   ```
   If you do not have `wget` installed, you can install it with:
   ```bash
   sudo apt-get install wget
   ```
1. The fingerprint should be `35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3`. You may check it with the following command:
   ```bash
   gpg -n -q --import --import-options import-show /etc/apt/keyrings/packages.mozilla.org.gpg | awk '/pub/{getline; gsub(/^ +| +$/,""); if($0 == "35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3") print "\nThe key fingerprint matches ("$0").\n"; else print "\nVerification failed: the fingerprint ("$0") does not match the expected one.\n"}'
   ```
1. Next, add the Mozilla APT repository to your sources list [²](https://askubuntu.com/a/1516224):
   ```bash
   echo '
   Types: deb
   URIs: https://packages.mozilla.org/apt
   Suites: mozilla
   Components: main
   Signed-By: /etc/apt/keyrings/packages.mozilla.org.gpg
   ' | sudo tee /etc/apt/sources.list.d/mozilla.sources
   ```
1. Configure APT to prioritize packages from the Mozilla repository:
   ```bash
   echo '
   Package: firefox*
   Pin: origin packages.mozilla.org
   Pin-Priority: 1000
   ' | sudo tee /etc/apt/preferences.d/mozilla
   ```
1. Remove existing Firefox installations
   ```
   sudo snap remove firefox
   sudo apt remove firefox
   ```
1. Update your package list and install the Firefox .deb package:
   - Firefox Developer Edition
     ```bash
     # Firefox Developer Edition
     sudo apt update && sudo apt install firefox-devedition
     ```
   - Firefox
     ```bash
     # Firefox
     sudo apt update && sudo apt install firefox
     ```
   - Firefox Beta
     ```bash
     # Firefox Beta (icon is the same as non beta version)
     sudo apt update && sudo apt install firefox-beta
     ```
   - Firefox Nightly
     ```bash
     # Firefox Nightly
     sudo apt update && sudo apt install firefox-nightly
     ```
