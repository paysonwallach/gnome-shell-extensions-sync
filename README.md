# Extensions Sync

Syncs gnome shell extensions and their configurations across all gnome installations with the help of gist

![SS](https://i.imgur.com/2vJ89Zo.jpg)

## Dependencies

* This extension depends on [gxml](https://gitlab.gnome.org/GNOME/gxml.git)

## Installation

### For ubuntu
```bash
curl https://raw.githubusercontent.com/oae/gnome-shell-extensions-sync/master/installer.sh | bash
```

### For Fedora
```bash
#!/bin/bash

sudo dnf install -y vala intltool libgee-devel libxml2-devel

rm -rf /tmp/gxml
git clone https://gitlab.gnome.org/GNOME/gxml.git --branch 0.16.3 /tmp/gxml
cd /tmp/gxml
./autogen.sh
./configure --prefix=/usr/
make
sudo make install

rm -rf /tmp/gnome-shell-extensions-sync
git clone https://github.com/oae/gnome-shell-extensions-sync.git /tmp/gnome-shell-extensions-sync
cd /tmp/gnome-shell-extensions-sync
make install
busctl --user call org.gnome.Shell /org/gnome/Shell org.gnome.Shell Eval s 'Meta.restart("Restarting…")'
make enable

```

### For others

* You can install it from link below
https://extensions.gnome.org/extension/1486/extensions-sync/

## Usage

1. Create a new gist from [here](https://gist.github.com/) I suggest you make it secret.
2. Create a new token from [here](https://github.com/settings/tokens/new). Only gist permission is needed since we edit the gists.
3. Open extension settings and fill gist id from first step and gist token from second step.
4. Enjoy!

## Notes

* Downloading from gist will do 3 things.
  - It will remove all extensions that are not exist in the gist.
  - It will install extensions that are listed in gist and update their settings.
  - It will update all the settings of installed the extensions.
  
* Uploading to gist will dump all the settings of the installed extensions(enabled/disabled) and put them in the gist with the below structure
```json
{
  "description": "Extensions sync",
  "files": {
    "syncSettings": {
      "content": {
        "lastUpdatedAt": "time",
      }
    },
    "extensions": {
      "content": {
        "extension1": {
          "schema1": "schema1 settings",
          "schema2": "schema2 settings",
        },
        "extension2": {
          "schema1": "schema1 settings",
          "schema2": "schema2 settings",
        },
      }
    }
  }
}
```

